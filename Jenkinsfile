pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Validate Application') {
            steps {
                sh 'test -f index.html'
                sh 'test -f Dockerfile'
                echo 'Application files validated successfully.'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t employee-dashboard:1.0 .'
            }
        }

        stage('Deploy Docker Container') {
            steps {
                sh '''
                    docker rm -f employee-dashboard-container || true
                    docker run -d \
                    --name employee-dashboard-container \
                    -p 8083:80 \
                    employee-dashboard:1.0
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh 'docker ps'
                sh 'curl -f http://localhost:8083'
            }
        }
    }

    post {
        success {
            echo 'Employee Dashboard Docker deployment successful!'
        }

        failure {
            echo 'Docker deployment failed. Check console output.'
        }
    }
}

