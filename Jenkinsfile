pipeline {
    agent any
    environment {
        DEPLOY_SERVER = 'ubuntu@54.224.210.19'  // Replace with your server's SSH user and IP
        DEPLOY_PATH = '/var/www/html/'   // Path where the PHP application will be deployed
    }
    stages {
        stage('Checkout Code') {
            steps {
                // Checkout your code from Git or another source
                git 'https://github.com/Shivachaithanya26/E-commerceApplication.git'
            }
        }
        stage('Deploy to Server') {
            steps {
                // Use SCP to copy the code files to the /var/www/html/ directory
                sh """
                scp -r * ${DEPLOY_SERVER}:${DEPLOY_PATH}
                """
            }
        }
        stage('Set Permissions') {
            steps {
                // Ensure correct file permissions for the web server
                sh """
                ssh ${DEPLOY_SERVER} 'sudo chown -R www-data:www-data ${DEPLOY_PATH} && sudo chmod -R 755 ${DEPLOY_PATH}'
                """
            }
        }
        stage('Restart PHP-FPM') {
            steps {
                // Restart PHP-FPM to apply the changes
                sh """
                ssh ${DEPLOY_SERVER} 'sudo systemctl restart php-fpm'
                """
            }
        }
    }
    post {
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
