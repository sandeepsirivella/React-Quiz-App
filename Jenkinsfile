pipeline {
    agent any

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
                echo 'Building Docker image from ./Dockerfile...'
                sh 'docker build -t $DOCKER_IMAGE -f ./Dockerfile .'
                echo 'Running Docker container...'
                sh 'docker run -d --name $APP_NAME -p 8080:8080 $DOCKER_IMAGE || true'
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
