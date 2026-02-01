pipeline {
  agent any

  environment {
    IMAGE_NAME = "ci-cd-demo"
    CONTAINER_NAME = "ci-cd-demo"
    HOST_PORT = "8090"
    CONTAINER_PORT = "80"
  }

  stages {
    stage('Docker sanity check') {
      steps {
        sh 'docker version'
        sh 'docker ps'
      }
    }

    stage('Build image') {
      steps {
        sh 'docker build -t $IMAGE_NAME .'
      }
    }

    stage('Stop old container') {
      steps {
        sh 'docker rm -f $CONTAINER_NAME || true'
      }
    }

    stage('Run container') {
      steps {
        sh '''
          docker run -d \
            --name $CONTAINER_NAME \
            -p $HOST_PORT:$CONTAINER_PORT \
            $IMAGE_NAME
        '''
      }
    }
  }
}
