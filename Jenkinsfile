pipeline {
    agent any
    stages {
        stage('Build and tag images') {
            steps {
                sh 'sudo docker build -t cmarin001/my-frontend:latest .'
                sh 'sudo docker tag cmarin001/my-frontend:latest ghcr.io/cmarin001/my-frontend:latest'
            }
        }
        stage('Push images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-docker-credentials', passwordVariable: 'TOKEN', usernameVariable: 'USERNAME')]) {
                    sh 'sudo docker login ghcr.io -u cmarin001 -p $TOKEN'
                    sh 'sudo docker push ghcr.io/cmarin001/my-frontend:latest'
                }
            }
        }
        stage('Clean up old containers') {
            steps {
                script {
                    def containers = sh(script: 'sudo docker ps -q -f ancestor=my-frontend', returnStdout: true).trim()
                    if (containers) {
                        sh 'sudo docker stop ${containers}'
                        sh 'sudo docker rm ${containers}'
                    }
                }
            }
        }
        stage('Run new image') {
            steps {
                sh 'sudo docker run -d --name my-frontend -p 80:80 ghcr.io/cmarin001/my-frontend:latest'
            }
        }
    }
}

