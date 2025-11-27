pipeline {
    agent any

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
    }
}
