pipeline {
    agent any

    environment {
        DOCKER_BUILDKIT = "1"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SJK3051/summer-of-code-2023.git'
            }
        }

        stage('Build Services') {
            steps {
                echo "Building all services with Docker Compose..."
                sh 'docker compose build'
            }
        }

        stage('Run Containers') {
            steps {
                echo "Starting containers..."
                sh 'docker compose up -d'
            }
        }

        stage('Health Checks') {
            steps {
                sh '''
                echo "Checking Backend..."
                curl -f http://localhost:8000/ || exit 1

                echo "Checking ML Service..."
                curl -f http://localhost:5000/ || exit 1

                echo "Checking Frontend..."
                curl -f http://localhost:3000/ || exit 1
                '''
            }
        }
    }

    post {
        always {
            sh 'docker compose down'
        }
    }
}
