pipeline {
    agent any

    stages{
        stage ('BuildImage-A') {
            steps {
                script {
                    dockerapp = docker.build("henrique77/appa", '-f ./appa ./app')
                }  
            }
        } 
    }
}