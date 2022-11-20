pipeline{
      agent {label 'slave'}
      options{
          buildDiscarder(logRotator(daysToKeepStr: '7'))
          disableConcurrentBuilds()
          timeout(time: 2, unit : 'MINUTES')
          retry(3)
      }
      parameters{
          string(name: 'BRANCH', defaultValue: 'master')
          booleanParam(name: 'Demo', defaultValue: false )
          choice(name: 'OPERATION', choices: ['A', 'S', 'M', 'D'])
      }
      triggers{
          cron('H */4 * * *')
          pollSCM('H */4 * * *')
      }
      tools{
          maven 'maven3.8'
      }
      environment{
          ECS_CLUSTER  = "VOTE"
      }
      stages{
          stage("Git Checkout"){
              steps{
              checkout scm
              }
          }
          stage("Parallel Stages"){
              parallel{
                  stage('Build Docker Image'){
                      steps{
                          sh 'cd vote && sudo docker build . -t  483718772154.dkr.ecr.us-east-1.amazonaws.com/vote:${BUILD_NUMBER}'
                          sh 'sudo docker push  483718772154.dkr.ecr.us-east-1.amazonaws.com/vote:${BUILD_NUMBER}'
                      }
                  }
                  stage("Third Stage"){
                      steps{
                          sh "echo linux"
                          sh "sleep 10"
                      }
                  }
                  stage("Fourth Stage"){
                      steps{
                          sh "echo linux"
                          sh "sleep 10"
                      }
                  }
              }
          }
  
      }
      post{
          always{
              echo "Running always"
          }
      }
  }
