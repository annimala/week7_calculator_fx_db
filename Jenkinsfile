pipeline {

    tools {
        maven 'Maven3'
    }

    environment {
          PATH = "C:\\Program Files\\Docker\\Docker\\resources\\bin;${env.PATH}"
          DOCKERHUB_CREDENTIALS_ID = 'Docker_Hub'
          DOCKERHUB_REPO = 'annialanen/calc_test'
          DOCKER_IMAGE_TAG = 'v1'
      }
    agent any
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/annimala/week7_calculator_fx_db.git'
            }
        }
        stage('Build') {
            steps {
                bat 'mvn clean install' // sh for linux and ios
            }
        }
         stage('Build Docker Image') {
              steps {
                 script {
                     docker.build("${DOCKERHUB_REPO}:${DOCKER_IMAGE_TAG}")
                 }
              }
         }

         stage('Push Docker Image to Docker Hub') {
              steps {
                  script {
                      docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS_ID) {
                          docker.image("${DOCKERHUB_REPO}:${DOCKER_IMAGE_TAG}").push()
                      }
                  }
              }
         }

    }
}