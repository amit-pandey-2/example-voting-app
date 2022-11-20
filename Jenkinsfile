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
        stage("First Stage"){
            steps{
                sh "echo hello"
            }
        }
        stage("Parallel Stages"){
            parallel{
                stage("Second Stage"){
                    agent {label 'windows'}
                    steps{
                        sh "echo windows"
                        sh "sleep 10"
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
