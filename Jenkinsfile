pipeline {
  agent {
    label 'slave'
  }
  stages {
    stage('Git Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Image') {
      parallel {
        stage('Build Docker Image') {
          steps {
            sh 'cd vote && sudo docker build . -t   483718772154.dkr.ecr.us-east-1.amazonaws.com/vote:${BUILD_NUMBER}'
            sh 'sudo docker push 483718772154.dkr.ecr.us-east-1.amazonaws.com/vote:${BUILD_NUMBER}'
          }
        }
    }
}
