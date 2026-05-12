pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t mywebsite .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                docker stop mycontainer || true
                docker rm mycontainer || true
                '''
            }
        }

        stage('Run Container') {
            steps {
                sh 'docker run -d -p 8080:80 --name mycontainer mywebsite'
            }
        }

    }

    post {
        always {
            cleanWs()
        }
    }
}