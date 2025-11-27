pipeline {
    agent any

    environment {
        BACKEND_IMAGE = 'tempproject-backend:latest'
        FRONTEND_IMAGE = 'tempproject-frontend:latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "Starting checkout..."
                git branch: 'main',
                    credentialsId: 'github-tempproject',
                    url: 'https://github.com/dharun-Siva/TempProject.git'
                sh 'ls -la'
            }
        }

        stage('Build Backend Docker Image') {
            steps {
                echo "Building backend Docker image..."
                sh 'docker build -t ${BACKEND_IMAGE} ./backend'
            }
        }

        stage('Build Frontend Docker Image') {
            steps {
                echo "Building frontend Docker image..."
                sh 'docker build -t ${FRONTEND_IMAGE} ./frontend'
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                echo "Deploying with Docker Compose..."
                sh 'docker-compose down'
                sh 'docker-compose up -d'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
