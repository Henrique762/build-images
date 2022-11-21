pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages{
        stage ('BuildImage-A') {
            steps {
                script {
                    dockerapp = docker.build("henrique77/appa", '-f ./appa/Dockerfile ./appa')
                }  
            }
        }

        stage {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage ('Push Image A') {
            steps {
                script {
                        dockerapp.push('latest')
                }
            } 
        }    
    }
}