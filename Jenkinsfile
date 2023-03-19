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
        stage('Build Jar'){
            steps {
                sh 'mvn clean package'
            }
        }
        // stage('SonarQube Code Analysis'){
        //     steps {
        //         sh 'mvn sonar:sonar'
        //     }
        // }
        // stage('Upload To Nexus'){
        //     sh 'mvn deploy'
        // }

    }

}


