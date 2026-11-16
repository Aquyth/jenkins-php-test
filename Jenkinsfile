pipeline{
    agent any

    environment {
        IMAGE_NAME = "php-login-app"
        CONTAINER_NAME = "php-login-app"
    }
    stages{
        stage('1. Git Checkout'){
            steps{
                script{
                    echo 'Downloading PHP source code'[cite: 1]
                    checkout scm[cite: 1, 2]
                }
            }
        }
        stage('2. PHP Syntax Test'){
            steps{
                sh '''
                    docker run --rm -v "$WORKSPACE":/app -w /app php:8.4-cli \
                    sh -c 'find . -name "*.php" -not -path "./vendor/*" \
                    -print0 | xargs -0 -r -n1 php -l'
                '''
            }
        }
        stage('3. Docker build'){
            steps{
                sh '''
                    docker compose build web
                '''[cite: 2]
            }
        }
        stage('4. Deploy Application'){ // Fixed 'stgage' to 'stage'
            steps{
                sh '''
                    docker compose up -d
                '''[cite: 3]
            }
        }
    }
}