pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/ravdy/nodejs-demo.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t pramod8788/nodeapp .'
            }
        }
        stage('login to dockerhub') {
            steps{
                script {
                    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhubpwd')]) { 
                    sh 'docker login -u pramod8788 -p ${dockerhubpwd}'
                    }
               
                }
            }
        }
        stage('push image') {
            steps{
                script {
                  sh 'docker push pramod8788/nodeapp'
                }
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}

