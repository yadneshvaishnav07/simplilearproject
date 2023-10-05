pipeline {
    agent any
    stages {
        stage('Create Docker Image') {
            steps {
                sh '''
                withDockerRegistry([ credentialsId: "docker", url: "" ])
                if [ "$(docker images -q jenkins)" ]; then
                    docker rmi -f Jenkins
                fi
                sudo docker build -t jenkins -f Dockerfile .
                sudo docker push jenkins
                '''
            }
        }
        stage('Deploy') {
            steps {
                sh 'sudo docker run -d -p 8095:8080 Jenkins'
            }
        }
    }
    post {
        success {
            echo 'Deployment successful!'
        }
    }
}
