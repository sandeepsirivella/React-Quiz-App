pipeline {
    agent any

    tools {
        nodejs "NodeJS"
        dockerTool "docker"

    }

    environment {
        APP_NAME = "React-Quiz-App"
        DOCKER_IMAGE = "$APP_NAME:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/md-kawsar-ali/React-Quiz-App.git'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh 'npm install && npm run build'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test'
            }
        }
        stage('Docker Build & Run') {
            steps {
                sh """
                docker build -t maa:1 .
                docker run -d -it -p 6061:5000 maa:1 
                """
            }
        }
        stage('Deploy') {
            steps {
                echo 'Application is now running inside Docker container.'
            }
        }
    }

    post {
        success {
            echo '✅ Pipeline succeeded!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
