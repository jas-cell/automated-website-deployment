pipeline {
  agent any

  environment {
    IMAGE_NAME = "ci-cd-demo"
    CONTAINER_NAME = "ci-cd-demo"
    HOST_PORT = "8090"
    CONTAINER_PORT = "80"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t $IMAGE_NAME:latest .'
      }
    }

    stage('Deploy Container') {
      steps {
        sh '''
          docker rm -f $CONTAINER_NAME || true
          docker run -d \
            --name $CONTAINER_NAME \
            -p $HOST_PORT:$CONTAINER_PORT \
            $IMAGE_NAME:latest
        '''
      }
    }

    stage('Smoke Test') {
      steps {
        sh '''
          sleep 2
          curl -f http://localhost:$HOST_PORT
        '''
      }
    }
  }

  post {
    success {
      echo "Deployment successful 🚀"
    }
  }
}
