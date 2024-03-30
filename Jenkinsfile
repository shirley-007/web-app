pipeline {
    agent any

    tools {
        maven "maven3.9.6"

    }
    stages {
        stage ("Git clone") {
            steps {
                git branch: 'main', url: 'https://github.com/shirley-007/web-app.git'
            }
        }
        stage ("Build with maven") {
            steps {
                sh '''
                mvn clean
                mvn test
                mvn package
                '''
            }

        }
    }
}