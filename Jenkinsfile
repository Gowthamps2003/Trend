pipeline {
    agent any

    stages {

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t gowthamps2003/trend-app:latest .'
            }
        }

        stage('Push to DockerHub') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKER_USER',
                        passwordVariable: 'DOCKER_PASS'
                    )
                ]) {
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                    sh 'docker push gowthamps2003/trend-app:latest'
                }
            }
        }

        stage('Deploy to EKS') {
            steps {
                sh 'kubectl rollout restart deployment trend-app'
            }
        }
    }
}
