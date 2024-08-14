pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        AWS_REGION = 'us-east-2'
        BUCKET_NAME = 'drkuniques3bucketname'
        AWS_CLI_DIR = "${env.WORKSPACE}/aws-cli" // Install AWS CLI in the workspace directory
    }

    stages {
        stage('Setup') {
            steps {
                script {
                    // Install AWS CLI if not already installed
                    if (!fileExists("${AWS_CLI_DIR}/bin/aws")) {
                        sh 'curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"'
                        sh 'unzip -o awscliv2.zip'
                        sh "./aws/install -i ${AWS_CLI_DIR} -b ${AWS_CLI_DIR}/bin"
                    }
                }
            }
        }

        stage('Create S3 Bucket') {
            steps {
                script {
                    // Add AWS CLI to PATH
                    env.PATH = "${AWS_CLI_DIR}/bin:${env.PATH}"
                    
                    // Create the S3 bucket
                    sh """
                        aws s3api create-bucket --bucket ${BUCKET_NAME} --region ${AWS_REGION} --create-bucket-configuration LocationConstraint=${AWS_REGION}
                    """
                }
            }
        }

        stage('Verify S3 Bucket') {
            steps {
                script {
                    // Add AWS CLI to PATH
                    env.PATH = "${AWS_CLI_DIR}/bin:${env.PATH}"
                    
                    // Verify the S3 bucket creation
                    sh """
                        aws s3 ls | grep ${BUCKET_NAME}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'S3 bucket created successfully!'
        }
        failure {
            echo 'Failed to create S3 bucket.'
        }
    }
}
