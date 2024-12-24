pipeline {
    agent any

    environment {
        // Define AWS and Chef paths or variables
        CHEF_HOME = '/home/jenkins/.chef'
        AWS_REGION = 'eu-west-2'
        EC2_USER = 'ubuntu'
        EC2_HOST = 'ec2-13-41-159-25.eu-west-2.compute.amazonaws.com'
    }

    stages {
        stage('Checkout Code') {
            steps {
                script {
                    // Clone the Git repository containing the website
                    checkout scm
                }
            }
        }

        stage('Package Application') {
            steps {
                powershell '''
                Write-Host "Packaging application..."
                Compress-Archive -Path * -DestinationPath website.zip -Force
                '''
            }
        }
    }

    post {
        success {
            script {
                echo "Deployment completed successfully!"
            }
        }
        failure {
            script {
                echo "Deployment failed. Check logs for details."
            }
        }
    }
}
