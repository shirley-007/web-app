pipeline {
    agent any

    tools {
        maven "maven3.9.6"

    }

    environment {
        scanner_home = tool 'sonar5.0'
    }

    stages {
        stage ("Git clone") {
            steps {
                git branch: 'main', url: 'https://github.com/shirley-007/web-app.git'
            }
        }
        stage ("Build, Test, Package with maven") {
            steps {
                sh '''
                mvn clean
                mvn test
                mvn package
                '''
            }

        }
        stage ("Sonarqube Analysis") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar_id') {
                    sh "${scanner_home}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}