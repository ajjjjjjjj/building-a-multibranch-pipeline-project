@Library('janek-pipeline-library') _

def EXAMPLE = 'example :)'

pipeline {
    agent any

    environment {
        DISABLE_AUTH = 'true'
        DB_ENGINE    = 'sqlite'
    }

    parameters {
        string(name: "TEST", defaultValue: "Hello")
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
                        janek name: VERSION, env: "yyy"
                    }
                }
            }
        }
        stage('e2e test') {
            steps {
                script {
                    def version = lastSuccessfulBuild()
                    def e2eBuild = build job: "e2e-pipeline", parameters: [
                        string(name: "SERVICE", value: "colony-query"),
                        string(name: 'COLONY_COMMAND_VERSION', value: params.TEST)
                        //string(name: "project", value: 'tego typu')
                    ]
                    echo "e2e-pipeline result: ${e2eBuild.result}"
                    if (e2eBuild.result == 'SUCCESS') {
                        echo "e2e-pipeline finished alright"
                        // write version to file
                        // git add, commit -m "Updated ${SERVICE} to ${VERSION}", push
                    }
                }

            }
        }
    }
}
