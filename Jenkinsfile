pipeline {
  agent any
  
  stages {
    stage('Upload Image') {
      steps {
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'blueocean', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
          sh """
            mkdir -p ~/.aws
            echo "[default]" >~/.aws/credentials
            echo "[default]" >~/.boto
            echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >>~/.boto
            echo "aws_access_key_id = ${AWS_SECRET_ACCESS_KEY}" >>~/.boto
            echo "aws_access_key_id = ${AWS_ACCESS_KEY_ID}" >>~/.aws/credentials
            echo "aws_access_key_id = ${AWS_SECRET_ACCESS_KEY}" >>~/.aws/credentials
          """
        }
      }

      stage('Create blue deployment') {
        steps {
          ansiblePlaybook playbook: 'blue.yml', inventory: 'inventory'
        }
      }
    }
  }
}