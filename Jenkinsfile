pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages{
        stage ('BuildImage-A') {
            steps {
                script {
                    dockerappa = docker.build("henrique77/appa", '-f ./appa/Dockerfile ./appa')
                    dockerappb = docker.build("henrique77/appb", '-f ./appb/Dockerfile ./appb')
                }  
            }
        }

        stage ('Login Docker') {
            steps   {
                script {
                    sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                }
            }
        }

        stage ('Push Image A') {
            steps {
                script {
                        //docker.withRegistry('https://registry.hub.docker.com', 'dockerhub')
                            dockerappa.push('latest')
                            dockerappb.push('latest')
                }
            } 
        }    
    }
}