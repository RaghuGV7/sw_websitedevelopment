pipeline {
    agent any

    environment {
        // Define AWS and Chef paths or variables
        CHEF_HOME = '/home/jenkins/.chef'
        AWS_REGION = 'eu-west-2'
        EC2_USER = 'ubuntu'
        EC2_HOST = 'ec2-3-9-16-175.eu-west-2.compute.amazonaws.com'
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
                script {
                    echo "Packaging application..."
                    // Use Groovy's zip method or call shell commands
                    sh 'zip -r website.zip *'
                }
            }
        }

        stage('Upload Package to EC2') {
            steps {
                sshagent(['aws-ec2-key']) {
                    sh '''
                    echo "Uploading package to EC2 instance..."
                    scp -o StrictHostKeyChecking=no website.zip $EC2_USER@$EC2_HOST:/tmp
                    '''
                }
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
