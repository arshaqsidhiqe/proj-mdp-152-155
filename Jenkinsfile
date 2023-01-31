pipeline {
    agent { label 'linux' }
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        DOCKERHUB_CREDENTIALS = credentials('arshaqsidhiqe-dockerhub')
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t arshaqsidhiqe/java-app:latest .'
            }   
        }
        stage('login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push arshaqsidhiqe/java-app:latest'
            }
        }
    }
    post {
        always {
            sh 'docker logout'
        }
    }
}