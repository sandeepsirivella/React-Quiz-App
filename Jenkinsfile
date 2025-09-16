pipeline {
    agent any

    tools {
        nodejs "NodeJS"
        dockerTool "docker"

    }

    environment {
        APP_NAME = "madhu"
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
                echo "Building Docker image from Dockerfile..."
                sh "docker build -t $DOCKER_IMAGE -f Dockerfile ."
                echo 'Cleaning up old container (if exists)...'
                sh "docker rm -f $APP_NAME || true"
                echo 'Running new Docker container...'
                sh "docker run -d --name $APP_NAME -p 8080:8080 $DOCKER_IMAGE"
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
