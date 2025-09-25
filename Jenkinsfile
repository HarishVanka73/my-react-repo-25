pipeline {
    agent any

    environment {
		ECR_ACCOUNT_ID = 
		AWS_REGION = 
        IMAGE_REPO_NAME = 'my-react-app'
		VERSION = ''
    }

    stages {
        stage('Checkout') {
            steps {
                 git branch: 'main', url:'https://github.com/HarishVanka73/my-react-repo-25.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test' // Optional - if you have tests
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }
		stage('Docker  Build') {
            steps {  
                script {
                    env.ecrUrl = "${ECR_ACCOUNT_ID}.dkr.ecr.${AWS_REGION}.amazonaws.com"
                    env.imageTag = "v${VERSION}"
                    env.IMAGE_NAME = "${IMAGE_REPO_NAME}:${env.imageTag}"
      	            sh "docker build -t ${env.IMAGE_NAME} ."   
                }
            }
        }

       
        stage('Push Docker Image to ECR') {
            steps {
                script {
                    sh """
                         aws ecr get-login-password --region ${AWS_REGION} | docker login --username AWS --password-stdin ${env.ecrUrl}
                         docker tag ${env.IMAGE_NAME} ${env.ecrUrl}/$IMAGE_REPO_NAME:${env.imageTag}
                         docker push ${env.ecrUrl}/$IMAGE_REPO_NAME:${env.imageTag}
                       """
                }
            }
        }
		
        stage('Deploy') {
            steps {
                echo "Deploy stage - Define your deployment here (e.g., Kubernetes, SSH, etc.)"
            }
        }
    }
}
