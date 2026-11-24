
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
        stage('Secret Text Test') {
    steps {
        withCredentials([
            string(
                credentialsId: 'shopeaseapitoken',
                variable: 'API_TOKEN'
            )
        ]) {
            sh '''
                echo "Secret Text credential loaded successfully"
                echo "API Token is available securely"
            '''
        }
    }
}
        stage('Credentials Test') {
    steps {
        withCredentials([
            usernamePassword(
                credentialsId: 'demo-credentials',
                usernameVariable: 'MY_USER',
                passwordVariable: 'MY_PASSWORD'
            )
        ]) {
            sh '''
                echo "Credentials loaded successfully"
                echo "Username: $MY_USER"
                echo "Password is protected"
            '''
        }
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
