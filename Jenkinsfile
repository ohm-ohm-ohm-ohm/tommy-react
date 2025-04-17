pipeline {
    agent any

    environment {
        IMAGE_NAME = "tommy-react"
        CONTAINER_NAME = "tommy-react-container"
        APP_PORT = "3000"
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/ohm-ohm-ohm-ohm/tommy-react.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $IMAGE_NAME .'
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    sh 'docker rm -f $CONTAINER_NAME || true'
                    sh 'docker run -d -p $APP_PORT:80 --name $CONTAINER_NAME $IMAGE_NAME'
                }
            }
        }
    }
}
