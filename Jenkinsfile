pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SJK3051/summer-of-code-2023.git'
            }
        }

        stage('Docker Compose Build') {
            steps {
                // Make sure version: is removed from docker-compose.yml
                sh 'docker compose config'
                sh 'docker compose build --no-cache'
            }
        }

        stage('Docker Compose Up') {
            steps {
                sh 'docker compose up -d'
            }
        }

        stage('Verify Services') {
            steps {
                sh 'docker compose ps'
            }
        }
    }

    post {
        success {
            echo '✅ Build & Deploy successful!'
        }
        failure {
            echo '❌ Build failed. Check logs.'
        }
        always {
            sh 'docker compose down || true'
        }
    }
}
