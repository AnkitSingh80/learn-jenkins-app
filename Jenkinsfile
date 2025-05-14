pipeline {
    agent any

    stages {
        stage('Build') {
            agent {
                docker {
                    image 'node:18-alpine'
                    reuseNode true
                }
            }

            steps {
                sh '''
                echo "Checking Node & npm versions"
                node -v
                npm -v
                echo "Cleaning environment"
                rm -rf node_modules
                npm cache clean --force
                echo "Installing dependencies"
                npm install
                echo "Building the app"
                npm run build
                ls -la 
                '''
            }
        }
    }
}
