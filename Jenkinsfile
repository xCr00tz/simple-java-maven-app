pipeline {
    agent any
        tools {
            maven 'maven'
            jdk 'jdk'
        }
        stages {
            stage('Build') {
                steps {
                    sh 'mvn clean package'
                }
            }
            stage('Sonarqube') {
                steps{
                    sh 'pwd && ls -lah'
                }
            }
            stage('Test') {
                steps {
                    sh 'mvn test'
                }
                post {
                    always {
                        junit 'target/surefire-reports/*.xml'
                    }
                }
            }
    }
}