pipeline {
    agent any

    stages {
        stage('Build and Test') {
            agent {
                docker {
                    // Use Debian-based image to avoid Alpine incompatibilities
                    image 'node:18-bullseye'
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
                npm ci

                echo "Building the app"
                npm run build

                echo "Running tests"
                npm test -- --ci --reporters=default --reporters=jest-junit

                echo "Listing test results"
                ls -la test-results
                '''
            }

            post {
                always {
                    junit 'test-results/junit.xml'
                }
            }
        }
    }
}
