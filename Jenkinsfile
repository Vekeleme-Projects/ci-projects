pipeline {
    agent any

    tools {
        maven 'maven-3.9.1'
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
        }
}