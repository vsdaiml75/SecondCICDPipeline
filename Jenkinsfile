pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/vsdaiml75/SecondCICDPipeline.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t secondcicdpipeline .'
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container
                    sh '''
                    docker stop secondcicdpipeline || true
                    docker rm secondcicdpipeline || true
                    '''

                    // Start a new container
                    sh '''
                    docker run -d --name secondcicdpipeline \
                    -v $(pwd):/app \
                    -w /app python:3.9-slim python main.py
                    '''
                }
            }
        }
    }
}
