pipeline {
    agent {
        docker {
            image 'python:3.11-slim'
            args '--user root'
        }
    }

    environment {
        APP_NAME = "flask-cicd-app"
        DOCKER_IMAGE = "flask-cicd-app:latest"
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Pulling latest code from GitHub...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing Python dependencies...'
                sh 'python3 -m pytest tests/ -v'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'pytest tests/ -v'
            }
            post {
                success { echo 'All tests passed!' }
                failure { echo 'Tests failed!' }
            }
        }
    }

    post {
        success { echo 'PIPELINE COMPLETED SUCCESSFULLY!' }
        failure { echo 'PIPELINE FAILED! Check logs above.' }
    }
}