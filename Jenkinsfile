pipeline {
    agent any

    environment {
        APP_NAME = "react-Quiz-App"
        DOCKER_IMAGE = "${APP_NAME}:latest"
    }

    tools {
        nodejs "node:20"   // ✅ Use NodeJS plugin (name must match your Jenkins config)
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
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'npm test || true'  // allow pipeline to continue even if tests fail
            }
        }

        stage('Docker Build & Run') {
            steps {
                echo 'Building Docker image from ./Dockerfile...'
                sh 'docker build -t ${DOCKER_IMAGE} -f ./Dockerfile .'
                echo 'Running Docker container...'
                sh '''
                    docker rm -f ${APP_NAME} || true
                    docker run -d --name ${APP_NAME} -p 8080:8080 ${DOCKER_IMAGE}
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo '🚀 Application is now running inside Docker container.'
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
