
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
            }
        }

        stage('Build') {
            steps {
                echo 'Building ShopEase application...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing ShopEase application...'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'

                    withSonarQubeEnv('SonarQube-Server') {
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

        stage('Deploy') {
            steps {
                sh '''
                    echo "Deploying ShopEase website to Nginx..."

                    cp "$WORKSPACE/index.html" /var/www/html/
                    cp "$WORKSPACE/styles.css" /var/www/html/

                    echo "ShopEase deployment completed!"
                '''
            }
        }
    }

    post {
        success {
            echo 'CI/CD Pipeline completed successfully!'
        }

        failure {
            echo 'CI/CD Pipeline failed!'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
