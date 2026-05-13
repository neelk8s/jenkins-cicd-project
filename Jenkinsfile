pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Pulling code from GitHub...'
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo 'Installing dependencies...'
                sh 'pip3 install -r requirements.txt --break-system-packages'
            }
        }

        stage('Run Tests') {
            steps {
                echo 'Running tests...'
                sh 'python3 -m pytest tests/ -v'
            }
            post {
                success { echo 'All tests passed!' }
                failure { echo 'Tests failed!' }
            }
        }
    }

    post {
        success { echo 'PIPELINE COMPLETED!' }
        failure { echo 'PIPELINE FAILED!' }
    }
}