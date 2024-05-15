pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building...'
                // 在这里添加构建步骤，例如：编译代码
            }
        }
        stage('Deploy to Dev') {
            steps {
                echo 'Deploying...'
                // 在这里添加部署步骤，例如：使用SSH部署到Azure VM
                sshagent(['<YOUR_SSH_CREDENTIAL_ID>']) {
                    sh '''
                    ssh -o StrictHostKeyChecking=no user@<YOUR_VM_IP> << EOF
                    cd /path/to/your/app
                    git pull origin main
                    # 在这里添加重启服务或其他部署操作
                    EOF
                    '''
                }
            }
        }
    }
}
