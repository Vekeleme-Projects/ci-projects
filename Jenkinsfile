pipeline {

    agent any

    tools {
        maven 'maven-3.9.1'
    }

    parameters {
        choice(name: 'Deploy', choices: ['Dev', 'Test', 'Prod'], description: 'Select Environment')
        booleanParam(name: 'executeTests', defaultValue: true, description: 'Select to either run test or not')
    }

    stages {
        stage ('init') {
            steps {
                script {
                    echo 'initializing scripts'
                    //gv = load "script.groovy"
                }
            }
        }

        stage ('version increment') {
            steps {
                script {
                    echo 'Version increasing'
                }
            }
        }     

        stage ('test') {
            when {
                expression {
                    params.executeTests == true
                }
            }
            steps {
                script {
                    echo 'Testing application'
                }
            }
        }

        stage ('build jar') {
            steps {
                script {
                    echo 'Building jar package'
                }
            }
        }

        stage ('code quality') {
            steps {
                script {
                    echo 'Performing code analysis'
                }
            }
        }

        stage ('Upload to Nexus') {
            steps {
                script {
                    echo 'Uploading to Nexus Artifactory'
                }
            }
        }        

        stage ('build/push docker image') {
            steps {
                script {
                    echo 'Building Docker Image '
                }
            }
        }

        stage ('deploy') {
            when {
                expression {
                    BRANCH_NAME = 'master'
                }
            }
            steps {
                script {
                    echo 'Deploying to Server'
                }
            }
        }

        stage ('commit changes') {
            steps {
                script {
                    echo 'Success! Commiting Version Changes'
                }
            }
        }        

    }



}