// pipeline {
//     agent any

//     stages {

//         stage('Checkout') {
//             steps {
//                 echo 'Checking out source code...'
//                 checkout scm
//             }
//         }

//         stage('Verify Files') {
//             steps {
//                 echo 'Checking project files...'
//                 sh 'ls -la'
//             }
//         }

//         stage('Build') {
//             steps {
//                 echo 'Preparing build files...'

//                 sh '''
//                 rm -rf build
//                 mkdir -p build
//                 cp index.html build/
//                 cp style.css build/
//                 '''
//             }
//         }

//         stage('Deploy to Nginx') {
//             steps {
//                 echo 'Deploying website to Nginx...'

//                 sh '''
//                 sudo cp -r build/* /var/www/html/
//                 '''
//             }
//         }

//     }

//     post {

//         success {
//             echo 'Website deployed successfully!'
//         }

//         failure {
//             echo 'Pipeline failed!'
//         }

//         always {
//             echo 'Cleaning workspace...'
//             cleanWs()
//         }
//     }
// }
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