pipeline {
    agent {
        docker {
            image 'docker:20.10' // Use an appropriate Docker image version
            args '-v /var/run/docker.sock:/var/run/docker.sock'
        }
    }
    stages {
        stage('Create Docker Image') {
            steps {
                sh '''
                if [ "$(docker images -q Jenkins)" ]; then
                    docker rmi -f Jenkins
                fi
                docker build -t Jenkins -f Dockerfile .
                docker push Jenkins
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker run -d -p 8095:8080 Jenkins'
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
        }
    }
}
