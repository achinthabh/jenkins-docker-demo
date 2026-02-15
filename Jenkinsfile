pipeline {
  agent any

  environment {
    IMAGE_NAME = "achintha-jenkins-demo"
    CONTAINER_NAME = "achintha-jenkins-demo"
    PORT = "8090"
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
        sh 'echo "Commit: $(git rev-parse --short HEAD)"'
      }
    }

    stage('Build Image') {
      steps {
        sh 'docker build --no-cache -t ${IMAGE_NAME}:latest .'
      }
    }

    stage('Deploy') {
      steps {
        sh '''
          docker rm -f ${CONTAINER_NAME} || true
          docker run -d --name ${CONTAINER_NAME} -p ${PORT}:80 ${IMAGE_NAME}:latest
        '''
      }
    }

    stage('Health Check') {
      steps {
        sh '''
          sleep 2
          curl -fsS http://localhost:${PORT} | head -n 5
        '''
      }
    }
  }

  post {
    always {
      sh 'docker ps --format "table {{.Names}}\t{{.Image}}\t{{.Status}}" | head -n 20'
    }
  }
}
