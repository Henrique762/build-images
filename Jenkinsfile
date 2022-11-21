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
                    dockerappc = docker.build("henrique77/appc", '-f ./appc/Dockerfile ./appc')
                    dockerappd = docker.build("henrique77/appd", '-f ./appd/Dockerfile ./appd')
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
                            dockerappc.push('latest')
                            dockerappd.push('latest')
                }
            } 
        }    
        stage ('Deploy-k8s') {
            steps {
                script{
                    withKubeConfig([credentialsId: 'kubeconfing', serverUrl: 'https://B8932378C2D948B945F153F72C0FD225.yl4.us-east-2.eks.amazonaws.com'])
                        sh 'kubectl apply -f ./k8s/deployments/appa_deployments.yaml'
                }
            }
        }
    
    
    }
}