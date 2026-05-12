pipeline {
    agent any

    stages {

        stage('Verify Files') {
            steps {
                echo 'Checking project files...'
                sh 'ls -la'
            }
        }

        stage('Build') {
            steps {
                echo 'Preparing build files...'

                sh '''
                mkdir -p build
                cp index.html build/
                cp style.css build/
                '''
            }
        }

        stage('Deploy to Nginx') {
            steps {
                echo 'Deploying website to Nginx...'

                sh '''
                sudo cp -r build/* /var/www/html/
                '''
            }
        }

    }

    post {

        success {
            echo 'Website deployed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }

        always {
            cleanWs()
        }
    }
}