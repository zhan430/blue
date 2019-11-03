pipeline {
  agent any
  
  stages {
    stage('Setup AWS Credentials') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'awscredential', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
          sh """
            mkdir -p ~/.aws
            echo "[default]" >~/.aws/credentials
            echo "[default]" >~/.boto3
            echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >>~/.boto3
            echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}" >>~/.boto3
            echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >>~/.aws/credentials
            echo "aws_secret_access_key = ${AWS_SECRET_ACCESS_KEY}" >>~/.aws/credentials
          """
        }
      }
    }

      stage('Create blue deployment') {
        steps {
          ansiblePlaybook playbook: 'blue.yml', inventory: 'inventory'
        }
      }
    }
}
