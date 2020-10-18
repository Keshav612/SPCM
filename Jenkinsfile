pipeline {
  environment {
    registry = "keshav1206/nodejs-mongo-docker-app"
    registryCredential = 'dockerhub'
    dockerImage = ''
  }
  agent any
  stages {
    stage('Fetching Code') {
      steps {
        git 'https://github.com/Keshav612/SPCM.git'
      }
    }
    stage('Build') {
       steps {
         sh 'docker build -t nodejs-mongo-docker-app .'
       }
    }
    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }
    stage('Deploying Image') {
      steps{
         script {
            docker.withRegistry( 'https://hub.docker.com/repository/docker/keshav1206/node-mongo', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
  }
}
