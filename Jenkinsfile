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

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'build/*'
            }
        }

    }

    post {

        success {
            echo 'Pipeline executed successfully!'
        }

        failure {
            echo 'Pipeline failed!'
        }

        always {
            echo 'Cleaning workspace...'
            cleanWs()
        }
    }
}