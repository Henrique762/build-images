pipeline {
    agent any

    stages{
        stage ('BuildImage-A') {
            steps {
                script {
                    dockerappa = docker.build("henrique77/appa", '-f ./appa/Dockerfile ./appa')
                }  
            }
        }
        stage ('Push Image A') {
            steps {
                script {
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                        dockerappa.push('latest')
                }
            } 
        }    
    }
}