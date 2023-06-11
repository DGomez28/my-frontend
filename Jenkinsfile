pipeline {
    agent any
    stages {
        stage('Build images') {
            steps {
                sh 'docker build -t ghcr.io/cmarin001/my-frontend:latest .'
            }
        }
        stage('Push images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-docker-credentials', passwordVariable: 'TOKEN', usernameVariable: 'USERNAME')]) {
                    sh 'docker login ghcr.io -u $USERNAME -p $TOKEN'
                    sh 'docker tag ghcr.io/cmarin001/my-frontend:latest ghcr.io/cmarin001/my-backend:latest'
                    sh 'docker push ghcr.io/cmarin001/my-frontend:latest'
                }
            }
        }
    }
}
