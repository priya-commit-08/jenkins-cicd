pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker_creds')
    }
    stages { 
        stage('SCM Checkout') {
            steps{
            git 'https://github.com/priya-commit-08/jenkins-cicd.git'
            }
        }

        stage('Build docker image') {
            steps {  
                sh 'docker build -t priyacommit08/nodeapp:$BUILD_NUMBER .'
            }
        }
            stage('Docker Login with Chosen Account') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: '4c43fcc2-beaf-4182-a3f9-9e19cc1e8de9',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh 'docker login -u $DOCKER_USER -p $DOCKER_PASS'
                }
            }
        }
        stage('push image') {
            steps{
                sh 'docker push priyacommit08/nodeapp:$BUILD_NUMBER'
            }
        }
        stage('Run Container') {
            steps {
                    sh "docker run -d --name node_app_$BUILD_NUMBER priya-commit-08/nodeapp:$BUILD_NUMBER"
            }
        }   
}
post {
        always {
            sh 'docker logout'
        }
    }
}
