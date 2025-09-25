pipeline {
    agent any

    environment {
        IMAGE_NAME = 'my-react-app'
        TAG = '${BUILD_NUMBER}'
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

        stage('Build Docker Image') {
            steps {
                sh "docker build -t ${IMAGE_NAME}:${TAG} ."
            }
        }

        

        stage('Deploy') {
            steps {
                echo "Deploy stage - Define your deployment here (e.g., Kubernetes, SSH, etc.)"
            }
        }
    }
}
