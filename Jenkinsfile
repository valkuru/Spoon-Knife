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
