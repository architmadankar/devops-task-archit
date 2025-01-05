pipeline {
    agent any
    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/architmadankar/devops-task-archit.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t sed/node-app .'
                }
            }
        }
        stage('Test Application') {
            steps {
                script {
                    sh 'docker run -d -p 3000:3000 --name test-node-app sed/node-app'
                    sh 'sleep 3'
                    sh 'curl localhost:3000 || exit 1'
                    sh 'docker stop test-node-app && docker rm test-node-app'
                }
            }
        }
        // stage('Push to Docker Hub') {
        //     steps {
        //         withDockerRegistry(credentialsId: 'dockerhub-credentials') {
        //             sh 'docker push sed/node-app'
        //         }
        //     }
        // }
    }
    post {
        always {
            script {
                sh 'docker system prune -f'
            }
        }
    }
}