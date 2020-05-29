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
                echo "Building..."
                script {
                    log.info("Janek")
                    log.warning "Hello!"
                }
            }
        }
        stage('When on master') {
            when {
                branch 'master'
            }
            steps {
                script {
                    log.info("I'm on " + branch)
                }
            }
        }
        stage('Go to Tests?') {
            agent none
            steps {
                script {
                    timeout(time: 1, unit: 'DAYS') {
                        input message: 'Do tests?'
                    }
                }
            }
        }
        stage('Test') {
            steps {
                janek()
                janek name: DB_ENGINE
                stefan 'Hello!'
            }
        }
    }
}
