pipeline {
    agent {
        docker {
            image 'node:18-alpine'
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    
    environment {
        DOCKER_HUB_CREDENTIALS = credentials('dockerhub-credentials')
        DOCKER_IMAGE = 'rahulb069/my-app'
        IMAGE_TAG = "${BUILD_NUMBER}"
    }
    
    stages {
        stage('Checkout') {
            steps {
                echo '📥 Checking out code...'
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                echo '🔨 Building application...'
                sh 'npm install'
                sh 'npm run build'
            }
        }
        
        stage('Test') {
            steps {
                echo '🧪 Running tests...'
                sh 'npm test'
            }
        }
        
        stage('Docker Build') {
            agent any
            steps {
                echo '🐳 Building Docker image...'
                sh """
                    docker build -t ${DOCKER_IMAGE}:${IMAGE_TAG} .
                    docker tag ${DOCKER_IMAGE}:${IMAGE_TAG} ${DOCKER_IMAGE}:latest
                """
            }
        }
        
        stage('Docker Login') {
            agent any
            steps {
                echo '🔐 Logging into Docker Hub...'
                sh 'echo $DOCKER_HUB_CREDENTIALS_PSW | docker login -u $DOCKER_HUB_CREDENTIALS_USR --password-stdin'
            }
        }
        
        stage('Docker Push') {
            agent any
            steps {
                echo '⬆ Pushing to Docker Hub...'
                sh """
                    docker push ${DOCKER_IMAGE}:${IMAGE_TAG}
                    docker push ${DOCKER_IMAGE}:latest
                """
            }
        }
        
        stage('Deploy') {
            agent any
            steps {
                echo '🚀 Deploying application...'
                sh """
                    docker stop my-app-container || true
                    docker rm my-app-container || true
                    docker run -d --name my-app-container -p 8080:8080 ${DOCKER_IMAGE}:latest
                """
            }
        }
    }
    
    post {
        always {
            echo '🧹 Cleaning up...'
            sh 'docker logout'
        }
        success {
            echo '✅ Pipeline executed successfully!'
        }
        failure {
            echo '❌ Pipeline failed!'
        }
    }
}
