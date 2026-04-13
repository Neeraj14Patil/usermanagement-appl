pipeline {
    agent any
    environment {
        DOCKER_USER = 'neeraj14patil' 
        IMAGE_NAME = 'usermanagement-application-image'
    }
    stages {
        stage('Checkout Source') {
            steps {
                checkout scm
            }
        }
        stage('Maven Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Docker Build & Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', 
                                 passwordVariable: 'PASS', 
                                 usernameVariable: 'USER')]) {
                    sh "docker build -t ${DOCKER_USER}/${IMAGE_NAME}:latest ."
                    sh "echo ${PASS} | docker login -u ${USER} --password-stdin"
                    sh "docker push ${DOCKER_USER}/${IMAGE_NAME}:latest"
                }
            }
        }
    }
}
