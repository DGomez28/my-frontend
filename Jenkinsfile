pipeline {
    agent any
    stages {
        stage('Build and tag images') {
            steps {
                sh 'sudo docker build -t ghcr.io/cmarin001/my-frontend:latest .'
                sh 'sudo docker tag ghcr.io/cmarin001/my-frontend:latest ghcr.io/cmarin001/my-frontend:latest'
            }
        }
        stage('Push images') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-docker-credentials', passwordVariable: 'TOKEN', usernameVariable: 'USERNAME')]) {
                    sh 'sudo docker login ghcr.io -u cmarin001 -p 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'
                    sh 'sudo docker push ghcr.io/cmarin001/my-frontend:latest'
                }
            }
        }
    }
}

