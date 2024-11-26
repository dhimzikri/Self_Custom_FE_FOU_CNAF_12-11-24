pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'dimas182/angular_app'
    }
    tools {
        nodejs "node14.16.1" // Replace with your Node.js version name from Jenkins
    }
    stages {
        stage('Install Dependencies') {
            steps {
                withCredentials([string(credentialsId: 'NPM_AUTH_TOKEN', variable: 'NPM_AUTH_TOKEN')]) {
                    // Set the npm registry URL
                    sh 'npm config set registry //registry.npmjs.org/'
                    // Set npm token
                    sh 'npm config set //registry.npmjs.org/:_authToken=${NPM_AUTH_TOKEN}'
                    sh 'npm install'
                }
            }
        }
    }
}
