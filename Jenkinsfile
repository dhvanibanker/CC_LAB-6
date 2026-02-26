pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/dhvanibanker/CC_LAB-6.git'
            }
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-app backend'
            }
        }

        stage('Run Backend Containers') {
            steps {
                sh '''
                docker rm -f backend1 backend2 || true
                docker run -d --name backend1 backend-app
                docker run -d --name backend2 backend-app
                '''
            }
        }

        stage('Run NGINX Load Balancer') {
    steps {
        sh '''
        docker rm -f nginx-lb || true
        docker network create lab-net || true

        docker network connect lab-net backend1 || true
        docker network connect lab-net backend2 || true

        docker build -t nginx-lb-image nginx

        docker run -d --name nginx-lb \
        --network lab-net \
        -p 80:80 \
        nginx-lb-image
        '''
         }
      }
    }
}
