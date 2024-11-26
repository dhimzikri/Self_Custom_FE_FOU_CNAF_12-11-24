pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'dimas182/angular_fe'
    }
    tools {
        nodejs "node14.16.1" // Replace with your Node.js version name from Jenkins
    }
    stages {
        stage('Setup .npmrc') {
            steps {
                withCredentials([string(credentialsId: 'NPM_AUTH_TOKEN', variable: 'NPM_AUTH_TOKEN')]) {
                    // Write the .npmrc file dynamically
                    sh '''
                    echo "//registry.npmjs.org/:_authToken=${NPM_AUTH_TOKEN}" > ~/.npmrc
                    '''
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build Application') {
            steps {
                sh 'npm run build'
            }
        }
    }
}
