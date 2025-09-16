pipeline {
    agent any

    tools {
        nodejs "node:20"

    }

    environment {
        APP_NAME = "React-Quiz-App"
        DOCKER_IMAGE = "$APP_NAME:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sandeepsirivella/React-Quiz-App.git'
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
                sh 'npm test || true'
            }
        }
        stage('Docker Build & Run') {
            steps {
                sh """
                if [ -f Dockerfile ]; then
                    docker build -t $DOCKER_IMAGE .
                    docker run -d -p 6061:80 $DOCKER_IMAGE
                else
                    echo "❌ Dockerfile not found!"
                    exit 1
                fi
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
