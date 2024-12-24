pipeline {
    agent any

    environment {
        // Define AWS and Chef paths or variables
        CHEF_HOME = '/home/jenkins/.chef'
        AWS_REGION = 'ap-south-1'
        EC2_USER = 'ubuntu'
        EC2_HOST = 'ec2-13-201-80-54.ap-south-1.compute.amazonaws.com'
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
}
