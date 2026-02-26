pipeline {
    agent any

    stages {

        stage('Checkout Code') {
    steps {
        git branch: 'main',
            url: 'https://github.com/dhvanibanker/CC_LAB-6.git'
           }
       } 

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker rm -f backend-pipeline || true'
                sh 'docker run -d --name backend-pipeline backend-app'
            }
        }
    }
}
