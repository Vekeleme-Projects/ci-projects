pipeline {
    agent any

    tools {
        maven 'maven-3.9.1'
    }
    environment {
        NEXUS_REPO_URL = '3.16.215.200:8081'
        NEXUS_PROTOCOL = 'http'
        NEXUS_VERSION = 'nexus3'
        NEXUS_REPO_NAME = 'vprofile-releases/'
        NEXUS_GRP_REPO = 'vprofile-group'
        NEXUS_CREDENTIAL_ID = 'nexus-credentials'
    }

    stages {
        stage('UNIT TEST') {
            steps {
            
                sh 'mvn test'
                }
            }

        stage('BUILD JAR') {
            steps {
                sh 'mvn clean package'
                }
        }

        stage ('CODE ANALYSIS') {
            environment {
                sonarScanner = tool 'sonar-4.8.0'
            }
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-token') {
                        sh 'mvn sonar:sonar'
                    }
                    timeout(time: 5, unit: 'MINUTES') {
                        waitForQualityGate abortPipeline: true
                    }
                }
            }
        }

         stage ('Upload to Nexus') {
            steps {
                script {
                    echo 'Uploading to Nexus Artifactory'
                    pom = readMavenPom file: "pom.xml";

                    nexusArtifactUploader artifacts: [
                        [artifactId: 'pom.artifactId',
                         classifier: '',
                         file: "target/${pom.artifactId}-${pom.version}.war",
                         type: 'pom.packaging']
                         ],
                         credentialsId: NEXUS_CREDENTIAL_ID, 
                         groupId: 'pom.groupId',
                         nexusUrl: NEXUS_REPO_URL,
                         nexusVersion: NEXUS_VERSION,
                         protocol: NEXUS_PROTOCOL,
                         repository: NEXUS_REPO_NAME,
                         version: 'pom.version'

                }
            }
        }   

    }   

}