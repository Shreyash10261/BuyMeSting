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
            steps {
                echo "SAST stage (will configure after SonarQube setup)..."
            }
        }

        stage('DAST - OWASP ZAP') {
            steps {
                echo "DAST stage (will configure after deployment URL)..."
            }
        }
    }
}
