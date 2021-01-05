pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t merveilletchouda/node-app:${DOCKER_TAG}"
            }
        }
        stage ('DockerHub Push'){
           withCredentials([string(credentialsId: 'docker-hub', variable: 'DockerHubPwd')]) {
            sh "docker login -u merveilletchouda -p ${DockerHubPwd}"
            sh "Docker push merveilletchouda/nodeapp:${DOCKER_TAG}"
        }
            
        }
    }
}

def getDockerTag(){
    def tag = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}