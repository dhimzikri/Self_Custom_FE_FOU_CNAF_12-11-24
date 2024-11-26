pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'dimas182/angular_front'
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
                withCredentials([string(credentialsId: 'NPM_AUTH_TOKEN', variable: 'NPM_AUTH_TOKEN')]) {
                    // Configure npm to use the token
                    sh 'npm cache clean --force'
                    sh 'npm cache verify'
                    sh 'npm config set //registry.npmjs.org/:_authToken=${NPM_AUTH_TOKEN}'
                    // Install npm dependencies
                    sh 'npm login'
                    sh 'npm install --legacy-peer-deps'
                }
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
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    // Log in to Docker Hub
                    sh 'echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin'
                    // Push Docker image to the registry
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
