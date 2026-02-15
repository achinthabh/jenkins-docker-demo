pipeline {
    agent any

    stages {

        stage('Clone Repo') {
            steps {
                echo 'Cloning repository...'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build --no-cache -t achintha-pipeline-demo .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f achintha-pipeline-demo || true
                docker run -d --name achintha-pipeline-demo -p 8090:80 achintha-pipeline-demo
                '''
            }
        }

    }
}
