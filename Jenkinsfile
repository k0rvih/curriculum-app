pipeline {
  agent any
  environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub_id')
  }
  stages {
    stage('Checkout Code') {
      steps {
        git(url: 'https://github.com/k0rvih/curriculum-app', branch: 'dev')
      }
    }

    stage('Log') {
      steps {
        sh 'ls -la'
      }
    }

    stage('Build') {
      steps {
        sh 'docker build -f curriculum-front/Dockerfile -t k0rvih/curriculum-front:$BUILD_NUMBER .'
      }
    }

    stage('Log into Dockerhub') {
      steps {
        sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'                		
        echo 'Login Completed'
      }
    }

    stage('Push') {
      steps {
        sh 'docker push k0rvih/curriculum-front:$BUILD_NUMBER'
      }
    }

  }
}