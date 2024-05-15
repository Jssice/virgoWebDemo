pipeline {
    agent any
    environment {
        DEPLOY_DIR = '/var/www/html' // Nginx default document root
    }


    stages {
        stage('Clone Repository') {
            steps {
                // Clone the Git repository
                git 'https://github.com/Jssice/virgoWebDemo.git'
            }
        }
        stage('Install Nginx') {
            steps {
                // Install Nginx on the Azure VM
                sh """
                ssh -o StrictHostKeyChecking=no azure-user@your-vm-ip '
                sudo apt update
                sudo apt install nginx -y
                sudo systemctl start nginx
                sudo systemctl enable nginx
                exit
                '
                """
            }
        }
        stage('Build') {
            steps {
                // Add build steps if any (e.g., npm install for Node.js projects)
                echo 'Building the project...'
            }
        }
        stage('Test') {
            steps {
                // Add test steps if any (e.g., npm test for Node.js projects)
                echo 'Running tests...'
            }
        }
        stage('Deploy') {
            steps {
                // Add deployment steps
                // Default ${DEPLOY_DIR} is /var/www/html
                //adam.jia@nexushub.onmicrosoft.com@http://20.205.168.65
                echo 'Deploying the project...'
                sh """
                ssh -o StrictHostKeyChecking=no adam.jia@nexushub.onmicrosoft.com@http://20.205.168.65 '
                sudo rm -rf ${DEPLOY_DIR}/*
                sudo mkdir -p ${DEPLOY_DIR}
                exit
                '
                scp -o StrictHostKeyChecking=no -r * adam.jia@nexushub.onmicrosoft.com@http://20.205.168.65:${DEPLOY_DIR}
                ssh -o StrictHostKeyChecking=no adam.jia@nexushub.onmicrosoft.com@http://20.205.168.65 '
                sudo systemctl restart nginx
                exit
                '
                """
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
