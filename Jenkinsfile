pipeline {
    agent any
    environment {
        NPM_TOKEN = credentials('NPM_AUTH_TOKEN') // Reference Jenkins Credentials
    }
    stages {
        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm i -g @angular/cli@latest'
                    sh '''
                        echo "//registry.npmjs.org/:_authToken=$NPM_TOKEN" > ~/.npmrc
                        npm install
                    '''
                }
            }
        }
        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }
    }
}
