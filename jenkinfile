pipeline {
    agent any
    tools {
        'maven-3.9.1'
    }
    stages {
        stage('Unit Test'){
            sh 'mvn test'
        }
        stage('Build Jar'){
            sh 'mvn clean package'
        }
        stage('SonarQube Code Analysis'){
            sh 'mvn sonar:sonar'
        }
        // stage('Upload To Nexus'){
        //     sh 'mvn deploy'
        // }

    }

}


