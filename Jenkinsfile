pipeline {
    agent any

    environment {
        AWS_ACCESS_KEY_ID = credentials('aws-access-key-id')
        AWS_SECRET_ACCESS_KEY = credentials('aws-secret-access-key')
        AWS_REGION = 'us-east-2'
        BUCKET_NAME = 'drk-s3bucket-east'
    }

    stages {
        stage('Setup') {
            steps {
                script {
                    // Install AWS CLI if not already installed
                    if (!fileExists('/usr/local/bin/aws')) {
                        sh 'curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"'
                        sh 'unzip awscliv2.zip'
                        sh 'sudo ./aws/install'
                    }
                }
            }
        }

        stage('Create S3 Bucket') {
            steps {
                script {
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
