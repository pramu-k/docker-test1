pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        bat 'docker build -t myjava1 .'
        bat  'docker tag myjava1 %DOCKER_BFLASK_IMAGE%'
      }
    }
    stage('Test') {
      steps {
        bat 'docker run myjava1'
      }
    }
    stage('Deploy') {
      steps {
        withCredentials([usernamePassword(credentialsId: "a834979f-2059-4782-bb0f-7052fd233fca", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
          bat "echo \%DOCKER_PASSWORD% | docker login -u \%DOCKER_USERNAME% --password-stdin docker.io"
          bat 'docker push %DOCKER_BFLASK_IMAGE%'
        }
      }
    }
  }
  post {
    always {
      bat 'docker logout'
    }
  }
}
