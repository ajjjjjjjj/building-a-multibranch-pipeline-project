@Library('janek-pipeline-library') _

def EXAMPLE = 'example :)'

pipeline {
    agent any

    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }

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
                janek name: DB_ENGINE
                stefan this, 'Hello!'
            }
        }
    }
}
