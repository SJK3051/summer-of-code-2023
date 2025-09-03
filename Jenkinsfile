pipeline {
    agent any

    environment {
        COMPOSE_PROJECT_NAME = "myapp"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SJK3051/summer-of-code-2023.git'
            }
        }

        stage('Build Images') {
            steps {
                sh 'docker compose build'
            }
        }

        stage('Run Containers') {
            steps {
                sh 'docker compose up -d'
            }
        }

        stage('Verify Services') {
            steps {
                sh 'docker ps'
            }
        }
    }

    post {
        always {
            echo 'Cleaning up...'
            sh 'docker compose down || true'
        }
    }
}

