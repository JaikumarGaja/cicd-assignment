pipeline {
    agent any
    stages {
        stage('Pull Latest Code') {
            steps {
                // Jenkins tells the ubuntu user to navigate to the monorepo and pull the latest code
                sh '''
                sudo -u ubuntu bash -c "cd /home/ubuntu/cicd-assignment && git pull origin main"
                '''
            }
        }
        stage('Install Dependencies') {
            steps {
                // Install backend dependencies directly using the venv's pip
                sh '''
                sudo -u ubuntu bash -c "cd /home/ubuntu/cicd-assignment/backend && ./venv/bin/pip install -r requirements.txt"
                '''
                // Install frontend dependencies
                sh '''
                sudo -u ubuntu bash -c "cd /home/ubuntu/cicd-assignment/frontend && npm install"
                '''
            }
        }
        stage('Restart Applications') {
            steps {
                // Restart both PM2 processes to serve the new code
                sh '''
                sudo -u ubuntu pm2 restart flask-backend
                sudo -u ubuntu pm2 restart express-frontend
                '''
            }
        }
    }
}