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
                git credentialsId: "${GIT_CREDENTIALS}", url: 'https://github.com/dharun-Siva/TempProject.git'
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
                // Example (optional):
                // sh 'aws ecr get-login-password --region ap-south-1 | docker login --username AWS --password-stdin <your_account>.dkr.ecr.ap-south-1.amazonaws.com'
                // sh 'docker tag ${BACKEND_IMAGE} <your_account>.dkr.ecr.ap-south-1.amazonaws.com/${BACKEND_IMAGE}'
                // sh 'docker push <your_account>.dkr.ecr.ap-south-1.amazonaws.com/${BACKEND_IMAGE}'
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
}
