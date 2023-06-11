pipeline {
    agent any
    stages {
        stage('Build images') {
            steps {
                sh 'sudo docker build -t cmarin001/my-frontend:latest .'
            }
        }
        stage('Push images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-docker-credentials', passwordVariable: 'TOKEN', usernameVariable: 'USERNAME')]) {
                    sh 'sudo docker login ghcr.io -u $USERNAME -p $TOKEN 2> /dev/null'
                    sh 'sudo docker tag cmarin001/my-frontend:latest ghcr.io/cmarin001/my-frontend:latest'
                    sh 'sudo docker push ghcr.io/cmarin001/my-frontend:latest'
                }
            }
        }
    }
}

