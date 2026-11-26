
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub'
            }
        }

        stage('Build') {
            steps {
                echo 'Building ShopEase application'
                sh 'test -f index.html'
                sh 'test -f Dockerfile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running basic application tests'
                sh 'test -s index.html'
                sh 'grep -qi "<html" index.html'
                echo 'Basic tests passed'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'

                    withSonarQubeEnv('SonarQubeServer') {
                        sh """
                            ${scannerHome}/bin/sonar-scanner \
                            -Dsonar.projectKey=ShopEase \
                            -Dsonar.projectName=ShopEase \
                            -Dsonar.sources=. \
                            -Dsonar.sourceEncoding=UTF-8
                        """
                    }
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh '''
                    docker build -t shopease:latest .
                '''
            }
        }

        stage('Docker Deploy') {
            steps {
                sh '''
                    docker rm -f shopease-e2e || true

                    docker run -d \
                      --name shopease-e2e \
                      --restart unless-stopped \
                      -p 8082:80 \
                      shopease:latest
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                sh '''
                    sleep 5
                    curl --fail http://localhost:8082/
                '''
            }
        }
    }

    post {
        success {
            echo 'ShopEase End-to-End CI/CD completed successfully!'
        }
        failure {
            echo 'ShopEase CI/CD pipeline failed!'
        }
        always {
            echo 'Pipeline execution finished.'
        }
    }
}
