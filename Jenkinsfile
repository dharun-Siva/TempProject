pipeline {
    agent any

    environment {
        // GitHub credentials ID you created in Jenkins
        GIT_CREDENTIALS = 'github-tempproject'
        
        // Docker images
        BACKEND_IMAGE = 'tempproject-backend:latest'
        FRONTEND_IMAGE = 'tempproject-frontend:latest'
    }

    stages {
        stage('Checkout Code') {
            steps {
                // Specify the correct branch (main)
                git branch: 'main', credentialsId: "${GIT_CREDENTIALS}", url: 'https://github.com/dharun-Siva/TempProject.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                script {
                    sh 'docker build -t ${BACKEND_IMAGE} ./backend'
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                script {
                    sh 'docker build -t ${FRONTEND_IMAGE} ./frontend'
                }
            }
        }

        stage('Push to ECR / Local Registry') {
            steps {
                echo 'You can add AWS ECR login and push commands here if needed'
            }
        }

        stage('Deploy with Docker Compose') {
            steps {
                script {
                    sh 'docker-compose down'
                    sh 'docker-compose up -d'
                }
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Check logs!'
        }
    }
} // <- make sure this final closing brace exists
