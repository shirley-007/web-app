pipeline {
    agent any

    tools {
        maven "maven 3.9.6"

    }
    stages {
        stage ("Git clone") {
            steps {
                git branch: 'main', url: 'https://github.com/shirley-007/web-app.git'
            }
        }
    }
}