pipeline {
    agent any
    
    triggers {
        pollSCM('* * * * *') // Checks for commits every minute
    }

    stages {
        stage('Preparation') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS') {
                        sh 'docker stop samplerunning'
                        sh 'docker rm samplerunning'
                    }
                }
            }
        }

        stage('Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/JasperSpilliaert/cicd-sample-app.git']])
            }
        }
        
        stage('Build') {
            steps {
                build job: 'BuildSampleApp'
            }
        }
        
        stage('Results') {
            steps {
                build job: 'TestSampleApp'
            }
        }
    }
}