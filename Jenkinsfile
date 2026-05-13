pipeline {
    agent any

    environment {
        APP_NAME = "flask-cicd-app"
        DOCKER_IMAGE = "flask-cicd-app:latest"
    }

    stages {

        stage('Checkout') {
            steps {
                echo '=========================================='
                echo 'Pulling latest code from GitHub...'
                echo '=========================================='
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo '=========================================='
                echo 'Installing Python dependencies...'
                echo '=========================================='
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                echo '=========================================='
                echo 'Running automated tests...'
                echo '=========================================='
                sh 'pytest tests/ -v'
            }
            post {
                success { echo 'All tests passed!' }
                failure { echo 'Tests failed! Pipeline stopped.' }
            }
        }

        stage('Build Docker Image') {
            steps {
                echo '=========================================='
                echo 'Building Docker image...'
                echo '=========================================='
                sh 'docker build -t ${DOCKER_IMAGE} .'
            }
        }

        stage('Test Docker Container') {
            steps {
                sh '''
                    docker run -d -p 5003:5000 --name test-container ${DOCKER_IMAGE}
                    sleep 3
                    curl http://localhost:5003/health
                    docker stop test-container
                    docker rm test-container
                    echo "Container test passed!"
                '''
            }
        }

        stage('Deploy') {
            when { branch 'main' }
            steps {
                sh '''
                    docker stop ${APP_NAME} || true
                    docker rm ${APP_NAME} || true
                    docker run -d \
                        --name ${APP_NAME} \
                        -p 5002:5000 \
                        --restart unless-stopped \
                        ${DOCKER_IMAGE}
                    echo "Deployed successfully!"
                '''
            }
        }
    }

    post {
        success { echo 'PIPELINE COMPLETED SUCCESSFULLY!' }
        failure { echo 'PIPELINE FAILED! Check logs above.' }
    }
}