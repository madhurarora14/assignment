pipeline {
    agent any
    stages {
        stage('list repo files') {
            steps {
                script {
                    sh "ls"
                }
            }
        }
        stage('show working directory') {
            steps {
                script {
                    sh "pwd"
                }
            }
        }
        stage('creating build') {
            steps {
                script {
                    sh "./gradlew clean build"
                }
            }
        }
        stage('list build contents') {
            steps {
                script {
                    sh "ls build/libs"
                }
            }
        }
        stage ('remove old jar from Docker') {
            steps {
                script {
                    sh "sudo rm DOCKER/spring-boot-with-prometheus-0.1.0.jar"
                }
            }
        }
        stage('copy buid file to docker build context') {
            steps {
                script {
                    sh "sudo cp /home/jenkins/workspace/assignment/pipeline-assignment/build/libs/spring-boot-with-prometheus-0.1.0.jar DOCKER/"
                }
            }
        }
        stage('build docker image and pushing to dockerhub') {
            steps {
                script {
                    sh "cd DOCKER; sudo docker build -t 10141730/helloworld:v_${BUILD_NUMBER} ."
                    sh "sudo docker push 10141730/helloworld:v_${BUILD_NUMBER}"
                }
            }
        }
        stage('runn docker container for assignment') {
            steps {
                script {
                    sh "ssh -i /home/ubuntu/madhur.pem ubuntu@54.146.86.241 sudo docker pull 10141730/helloworld:v_${BUILD_NUMBER}"
                    sh "ssh -i /home/ubuntu/madhur.pem ubuntu@54.146.86.241 sudo docker kill hello-world"
                    sh "ssh -i /home/ubuntu/madhur.pem ubuntu@54.146.86.241 sudo docker rm hello-world"
                    sh "ssh -i /home/ubuntu/madhur.pem ubuntu@54.146.86.241 sudo docker run -it -p 8080:8080 --name hello-world -d 10141730/helloworld:v_${BUILD_NUMBER}"
                }
            }
        }
    }
}
