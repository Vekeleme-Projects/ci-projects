pipeline {
    agent any

    tools {
        maven 'maven-3.9.1'
    }
    environment {
        NEXUS_REPO_URL = 'http://3.16.215.200:8081'
        NEXUS_PROTOCOL = 'http'
        NEXUS_VERSION = 'Nexus 3'
        NEXUS_REPO_NAME = 'vprofile-releases'
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
                    def mavenPom = readMavenPom 'pom.xml'

                    nexusArtifactUploader artifacts: [
                        [artifactId: 'pom.aritfactId',
                         classifier: '',
                         file: "target/*.war",
                         type: 'pom.packaging']
                         ],
                         credentialsId: 'git-credentials', 
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