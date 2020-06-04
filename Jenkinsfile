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
                    currentBuild.description = "1.0-${BUILD_NUMBER}-${BRANCH_NAME}"
                    //currentBuild.id = "1.0-${BUILD_NUMBER}"
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
        stage('Stage with steps inside shared lib') {
            steps {
                sharedStep BRANCH_NAME
            }

        }
        /*stage('Go to Tests?') {
            agent none
            steps {
                script {
                    timeout(time: 1, unit: 'DAYS') {
                        input message: 'Do tests?'
                    }
                }
            }
        }*/
        stage('Test') {
            when {
                branch 'development'
            }
            parallel {
                stage ('Test janek') {
                    steps {
                        janek name: DB_ENGINE, env: "xxx"

                    }
                }
                stage ('Test stefan') {
                    steps {
                        stefan()
                    }
                }
            }
        }
        stage('e2e test') {
            steps {
                script {
                    def version = lastSuccessfulBuild()
                    echo "e2e-pipeline on version: ${version}"
                    //runE2ETests(version)
                    def e2eBuild = build job: "e2e-pipeline", parameters: [[$class: 'StringParameterValue', name: "version", value: version]
                    echo "e2e-pipeline result: ${e2eBuild.result}"
                }

            }
        }
    }
}
