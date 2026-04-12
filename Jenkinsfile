pipeline {
  agent any

  environment {
    IMAGE = "saurav6200907210/webmetricsx-frontend:${BUILD_NUMBER}"
  }

  stages {

    stage('Clone Code') {
      steps {
        git 'https://github.com/Saurav6200907210/webmetrics-e2e-devops-project.git'
      }
    }

    stage('Docker Login') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USER', passwordVariable: 'PASS')]) {
          sh 'echo $PASS | docker login -u $USER --password-stdin'
        }
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $IMAGE .'
      }
    }

    stage('Push Docker Image') {
      steps {
        sh 'docker push $IMAGE'
      }
    }

    stage('Deploy') {
      steps {
        echo "Skipping Kubernetes deployment (low resources)"
      }
    }

  }

  post {
    success {
      echo '✅ Build & Push Successful!'
    }
    failure {
      echo '❌ Pipeline Failed!'
    }
  }
}