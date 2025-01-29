pipeline {
    agent any

    environment {
        DEPLOY_DIR = "/var/www/html/E-commerceApplication"
        SERVER_USER = "ubuntu"
        SERVER_IP = "54.221.166.139"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', credentialsId: 'your-credentials-id', url: 'git@github.com:your-username/your-repo.git'
            }
        }

        stage('Deploy to Server') {
            steps {
                sshagent(['your-credentials-id']) {
                    sh """
                    ssh -o StrictHostKeyChecking=no your-user@your-application-server-ip << EOF
                    cd $DEPLOY_DIR
                    sudo git pull origin main
                    sudo composer install  # Modify based on your project (e.g., pip install, composer install)
                    sudo systemctl restart nginx  # Change to apache2, pm2, etc.
                    EOF
                    """
                }
            }
        }
    }
}
