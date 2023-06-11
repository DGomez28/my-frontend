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
                sh 'docker stop $(docker ps -q -f ancestor=cmarin001/my-frontend)'
                sh 'docker rm $(docker ps -a -q -f status=exited)'
            }
        }
        stage('Run new image') {
            steps {
                sh 'docker run -d --name my-frontend -p 8080:80 ghcr.io/cmarin001/my-frontend:latest'
            }
        }
    }
}

