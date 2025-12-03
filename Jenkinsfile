pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/Shreyash10261/BuyMeSting'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh '''
                npm install
                '''
            }
        }

        stage('Build Project') {
            steps {
                sh '''
                npm run build || true
                '''
            }
        }

        stage('Check Node Version') {
            steps {
                sh '''
                echo "Node version:"
                node -v
                npm -v
                '''
            }
        }

        stage('SAST - SonarQube') {
            environment {
                scannerHome = tool 'sonar-scanner'
            }
            steps {
                withSonarQubeEnv('LocalSonar') {
                    sh '''
                        ${scannerHome}/bin/sonar-scanner \
                        -Dsonar.projectKey=BuyMeSting \
                        -Dsonar.sources=. \
                        -Dsonar.host.url=http://localhost:9000
                    '''
                }
            }
        }

        stage('DAST - OWASP ZAP') {
            steps {
                echo "DAST stage (will configure after deployment URL)..."
            }
        }
    }
}
