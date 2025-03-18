pipeline {
    agent any
    environment {
        DOCKER_IMAGE = "docker-app:latest"
    }

    stages {
        stage('Checkout Code') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'github-padma', usernameVariable: 'GIT_USER', passwordVariable: 'GIT_TOKEN')]) {
                    git url: "https://$GIT_USER:$GIT_TOKEN@github.com/PadmavathyNarayanan/jenkins-docker-demo.git", branch: 'main'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 5001:5000 --name my-running-app $DOCKER_IMAGE'
            }
        }
    }

    post {
        success {
            echo "Build and container run successful!"
        }
        failure {
            echo "Build or container run failed."
        }
    }
}
