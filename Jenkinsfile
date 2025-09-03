pipeline {
    agent any

    environment {
        // Disable BuildKit Bake to avoid "file already closed" issues
        DOCKER_BUILDKIT = "0"
        COMPOSE_DOCKER_CLI_BUILD = "0"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/SJK3051/summer-of-code-2023.git'
            }
        }

        stage('Docker Compose Config Check') {
            steps {
                // Validate YAML syntax
                sh 'docker compose config'
            }
        }

        stage('Docker Compose Build Services') {
            steps {
                // Build each service individually to avoid long log delays
                sh 'docker compose build --progress=plain ml'
                sh 'docker compose build --progress=plain backend'
                sh 'docker compose build --progress=plain frontend'
                sh 'docker compose build --progress=plain app'
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
            sh 'docker compose logs --tail=50' // Show last 50 lines of logs on failure
        }
        always {
            sh 'docker compose down || true' // Cleanup containers
        }
    }
}
