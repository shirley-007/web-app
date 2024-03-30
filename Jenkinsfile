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
                    sh "${scanner_home}/bin/sonar-scanner -Dsonar.projectKey=webapp"
                    }
                }
            }
        }

        stage ("Upload to Nexus") {
            steps {
                nexusArtifactUploader artifacts: [[artifactId: 'maven-web-application', classifier: '', file: '/var/lib/jenkins/workspace/webapp-project/target/web-app.war', type: 'war']], credentialsId: 'nexus_id', groupId: 'com.mt', nexusUrl: '13.49.244.35:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'http://13.49.244.35:8081/repository/webapp-snapshot/', version: '3.1.2-SNAPSHOT'
            }
        }
    }
}