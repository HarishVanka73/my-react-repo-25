pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-react-app'
        TAG = 'latest'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 
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

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${TAG} ."
            }
        }

        stage('Push Docker Image') {
            when {
                expression { return env.DOCKER_HUB_USERNAME != null }
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh "echo $PASSWORD | docker login -u $USERNAME --password-stdin"
                    sh "docker tag ${IMAGE_NAME}:${TAG} $USERNAME/${IMAGE_NAME}:${TAG}"
                    sh "docker push $USERNAME/${IMAGE_NAME}:${TAG}"
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
