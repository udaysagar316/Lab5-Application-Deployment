
pipeline {
    agent any

    environment {
        DOCKER_EXE = 'C:/Users/uppar/AppData/Local/Programs/DockerDesktop/resources/bin/docker.exe'
    }

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
                bat '"%DOCKER_EXE%" build -t lab5-web-app:1.0 .'
            }
        }

        stage('Deploy Container') {
            steps {
                bat '"%DOCKER_EXE%" rm -f lab5-container || exit /b 0'
                bat '"%DOCKER_EXE%" run -d --name lab5-container -p 8081:80 lab5-web-app:1.0'
            }
        }

        stage('Verify Deployment') {
            steps {
                bat '"%DOCKER_EXE%" ps'
                bat 'curl.exe -f http://localhost:8081'
            }
        }
    }
}
