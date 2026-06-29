pipeline {
    agent any
    environment{
        DOCKER_CRED = credentials('DockerHub')
    }
    stages {
        stage('fetch_code') {
            steps {
                git branch: 'main', url: 'https://github.com/Saiyamjain1710/jenkins-demo.git'
            }
        }
        stage('build_image') {
            steps {
                sh 'docker build -t cheaterkookjr1/jenkins-app:${BUILD_NUMBER} .'
            }
        }
        stage('push-image') {
            steps {
                sh 'echo $DOCKER_CRED_PSW | docker login -u $DOCKER_CRED_USR --password-stdin'
                sh 'docker push cheaterkookjr1/jenkins-app:${BUILD_NUMBER}'
            }
        }
        stage('update_minikube') {
            steps {
                sh 'kubectl set image deployment/pd1 jenkins-app=cheaterkookjr1/jenkins-app:${BUILD_NUMBER}'
            }
        }
    }
}
