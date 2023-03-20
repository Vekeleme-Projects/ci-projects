pipeline {
    agent any
    tools {
        maven "maven-3.9.1"
    }
    stages {
        stage('Unit Test'){
            steps {
                sh 'mvn test'
            }   
        }
        stage('SonarQube Code Analysis'){
            environment {
                sonarScanner =  tool 'sonar-4.8.0'
            }
            steps {
                sh 'mvn sonar:sonar'
            }
        }
        stage('Build Jar'){
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Upload To Nexus'){
            sh 'mvn deploy'
        }

    }

}


