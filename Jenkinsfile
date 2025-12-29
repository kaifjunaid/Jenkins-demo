pipeline {
    agent any

    triggers {
        githubPush()   // Auto-trigger on every GitHub commit 
    }
  environment {
        APP_DIR = '/var/www/Finecart-app'
        PORT = '3000'
    }
    stages {

        stage('Clean Workspace') {
            steps {
                echo "Cleaning Jenkins workspace..."
                deleteDir()
            }
        }

        stage('Clone Repository') {
            steps {
                echo "Cloning the repository..."
                git branch: 'main', url: 'https://github.com/kaifjunaid/Jenkins-demo.git'
            }
        }

        stage('Deploy to EC2') {
            steps {
                echo "Deploying HTML website to EC2..."

                sh '''
                    sudo mkdir -p /var/www/finecart-app
                    sudo chown -R jenkins:jenkins /var/www/finecart-app

                    rsync -av --delete --exclude=.git ./ /var/www/finecart-app

                    echo "Deployment Completed Successfully!"
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed!"  
        }
    }
} 
