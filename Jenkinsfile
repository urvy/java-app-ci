pipeline {

    agent any
 
    environment {

        AWS_REGION = 'us-east-1'

        ECR_REPO = '854681582780.dkr.ecr.eu-north-1.amazonaws.com/my-java-app'

    }
 
    stages {

        stage('Checkout Code') {

            steps {

                git branch: 'main', url: 'https://github.com/urvy/java-app-ci.git'

            }

        }
 
        stage('Build with Maven') {

            steps {

                sh 'mvn clean install'

            }

        }
 
        stage('Build Docker Image') {

            steps {

                sh 'docker build -t my-app:latest .'

            }

        }
 
        stage('Login to Amazon ECR') {

            steps {

                withAWS(region: "${AWS_REGION}", credentials: 'aws-creds') {

                    sh """

                        aws ecr get-login-password --region ${AWS_REGION} | \

                        docker login --username AWS --password-stdin ${ECR_REPO}

                    """

                }

            }

        }
 
        stage('Push Docker Image to ECR') {

            steps {

                sh """

                    docker tag my-app:latest ${ECR_REPO}:latest

                    docker push ${ECR_REPO}:latest

                """

            }

        }

    }

}

 
