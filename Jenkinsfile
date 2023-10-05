pipeline {
    agent any
    stages {
        stage('Build and Push Docker Image') {
            steps {
                script {
                    // Checkout code from GitHub
                    git clone "https://github.com/yadneshvaishnav07/simplilearproject.git"

                    // Build and tag the Docker image
                    docker.build("yadnesh/your-app-name:${env.BUILD_NUMBER}")

                    // Push the Docker image to Docker Hub
                    docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        docker.image("yadnesh/your-app-name:${env.BUILD_NUMBER}").push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                // Pull and run the Docker image
                sh "docker pull yadnesh/your-app-name:${env.BUILD_NUMBER}"
                sh "docker run -d -p 80:80 yadnesh/your-app-name:${env.BUILD_NUMBER}"
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
        }
    }
}
