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
                sh 'docker build -t pramod8788/nodeapp:$BUILD_NUMBER .'
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
                  sh 'docker build -t pramod8788/my-nodeapp .'
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

