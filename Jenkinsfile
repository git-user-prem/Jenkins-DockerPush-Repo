pipeline {
    agent any

    environment {
        IMAGE_NAME = "nginx-modified"
        IMAGE_TAG = "p1"
    }

    stages {
        stage('Clone') {
            steps {
                git url: 'https://github.com/git-user-prem/Jenkins-DockerPush-Repo.git'  // or use local repo path
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    sh 'docker build -t dockerprem27/$IMAGE_NAME:$IMAGE_TAG .'
                }
            }
        }
     stage('Docker Login & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKERHUB_USER', passwordVariable: 'DOCKERHUB_PASS')]) {
                    sh '''
                        echo "$DOCKERHUB_PASS" | docker login -u "$DOCKERHUB_USER" --password-stdin
                        docker push dockerprem27/$IMAGE_NAME:$IMAGE_TAG
                    '''
                }
            }
        }

         stage('List Docker Images') {
             steps {
                 sh 'docker images'
            }
        }
    }
}
