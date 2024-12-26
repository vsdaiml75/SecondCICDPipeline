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
                bat 'docker build -t secondcicdpipeline .'
            }
        }
        stage('Run Docker Container') {
            steps {
                script {
                    // Stop and remove any existing container
                    bat '''
                    docker stop secondcicdpipeline || exit 0
                    docker rm secondcicdpipeline || exit 0
                    '''

                    // Start a new container
                    bat '''
                    docker run -d --name secondcicdpipeline \
                    -v %cd%:/app \
                    -w /app python:3.9-slim python main.py
                    '''
                }
            }
        }
    }
}
