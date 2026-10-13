
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Verify Source Files') {
            steps {
                bat 'dir'
                bat 'if not exist index.html exit /b 1'
                bat 'if not exist Dockerfile exit /b 1'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t lab5-web-app:1.0 .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat 'powershell -NoProfile -Command "$c = docker ps -aq --filter name=^lab5-container$; if ($c) { docker rm -f lab5-container }"'
                bat 'docker run -d --name lab5-container -p 8081:80 lab5-web-app:1.0'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat 'docker ps'
                bat 'curl.exe -f http://localhost:8081'
            }
        }
    }
}
