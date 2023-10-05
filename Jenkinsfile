pipeline {
    agent any
    stages {
        stage('Create Docker Image') {
            steps {
                script {
                    if (sh(script: 'docker images | grep -o "jenkins"', returnStatus: true) == 0) {
                        sh 'docker rmi -f jenkins'
                    }
                    sh 'docker build -t jenkins -f Dockerfile .'
                    sh 'docker push jenkins' // Push the Docker image to a Docker registry (e.g., Docker Hub)
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8095:8080 jenkins'
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
        }
    }
}
