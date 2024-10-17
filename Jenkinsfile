node {
    stage('Preparation') {
        catchError(buildResult: 'SUCCESS') {
            sh 'docker stop samplerunning'
            sh 'docker rm samplerunning'
        }
    }
    stage('Build') {
        build 'BuildSampleApp'
    }
    stage('Results') {
        build 'TestSampleApp'
    }
    stage('Deploy') {
        script {
            sh 'docker run -d -p 5050:80 --name samplerunning cicd-sample-app'
        }
    }
}