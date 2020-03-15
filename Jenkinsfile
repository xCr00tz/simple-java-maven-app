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
                environment {
                    scannerHome = tool 'SonarQube'
                }
                steps {
                    withSonarQubeEnv('sonarqube') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                    timeout(time: 10, unit: 'MINUTES') {
                        waitForQualityGate abortPipeline: true
                    }
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