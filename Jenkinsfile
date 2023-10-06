pipeline {
    agent any
    environment {
        DOCKER_REGISTRY_CREDENTIALS = credentials('project') // Specify your Docker Hub credentials ID here
        DOCKER_IMAGE_NAME = 'jenkins'
    }
    stages {
        stage('Create Docker Image') {
            steps {
                script {
                    if (docker.image(DOCKER_IMAGE_NAME).exists()) {
                        docker.image(DOCKER_IMAGE_NAME).remove()
                    }
                    docker.build(DOCKER_IMAGE_NAME, '-f Dockerfile .')
                    docker.withRegistry('', DOCKER_REGISTRY_CREDENTIALS) {
                        docker.image(DOCKER_IMAGE_NAME).push()
                    }
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
