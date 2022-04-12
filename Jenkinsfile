pipeline {
  environment {
    registry = '<ACCOUNT_ID>.dkr.ecr.<REGION>.amazonaws.com/jenkins-cicd'
    registryCredential = 'IAM_SAA'
    dockerImage = 'aws-ecr'
  }
  agent any
  stages {
    stage('Build docker image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Push image to ECR') {
        steps{
            script{
                docker.withRegistry("https://" + registry, "ecr:<REGION>:" + registryCredential) {
                    dockerImage.push()
                }
            }
        }
    }
  }
}
