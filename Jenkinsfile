pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Source code checkout completed'
            }
        }

        stage('Build') {
            steps {
                echo 'Building Spoon-Knife application'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing application'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
