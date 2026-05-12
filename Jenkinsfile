pipeline {
    agent any

    stages {

        stage('Verify Files') {
            steps {
                echo 'Checking files...'
                sh 'ls -la'
            }
        }

        stage('Build') {
            steps {
                echo 'Creating build folder...'

                sh '''
                mkdir -p build
                cp index.html build/
                cp style.css build/
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying website to Apache...'

                sh '''
                sudo cp -r build/* /var/www/html/
                '''
            }
        }

    }

    post {

        success {
            echo 'Deployment successful!'
        }

        failure {
            echo 'Pipeline failed!'
        }

        always {
            cleanWs()
        }
    }
}