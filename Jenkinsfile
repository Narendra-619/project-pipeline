pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                echo 'Cloning repository...'
                git 'YOUR_GITHUB_REPO_URL'
            }
        }

        stage('Verify Files') {
            steps {
                echo 'Checking project files...'
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