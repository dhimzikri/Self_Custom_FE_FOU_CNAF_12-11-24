pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'dimas182/angularjs-app'
    }
    tools {
        nodejs "node23.1.0" // Replace with your Node.js version name from Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm config set registry https://registry.npmjs.org/'
                sh 'npm install --force'
            }
        }
        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Docker Build') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }
        stage('Docker Push') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://hub.docker.com/u/dimas182']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }
        stage('Deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
