@Library('janek-pipeline-library') _

pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'echo "Hello world!"'
                script {
                    log.info("Janek")
                    log.warning "Hello!"
                }
            }
        }
        stage('Test') {
            steps {
                janek()
                janek('Stefan')
            }
        }
    }
}
