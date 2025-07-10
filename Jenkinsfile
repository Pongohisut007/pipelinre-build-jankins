pipeline {
    agent any

    stages {
        stage('Pull From Git') {
            steps {
                git branch: 'main', url: 'https://github.com/Pongohisut007/pipelinre-build-jankins.git'
            }
        }

        stage('Docker Compose Build') {
            steps {
                dir('client') {
                    sh 'docker-compose build'
                }
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_hub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                sh 'docker push pongphisut/jclient:latest'
            }
        }

        stage('Success') {
            steps {
                echo '✅ Deploy Successfully'
            }
        }
    }
}
