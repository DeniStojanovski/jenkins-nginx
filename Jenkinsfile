pipeline {
  agent any
  stages {
    stage('Clone repository') {
      steps {
        checkout scm
      }
    }

    stage('Build image') {
      steps {
        sh 'docker build -t your-dockerhub-username/jenkins-nginx:latest .'
      }
    }

    stage('Push image') {
      steps {
        withCredentials(bindings: [usernamePassword(credentialsId: 'dockerhub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
          sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
          sh 'docker push your-dockerhub-username/jenkins-nginx:latest'
        }

      }
    }

  }
}