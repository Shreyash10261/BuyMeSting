pipeline {
    agent any

    tools {
        nodejs 'node18'
    }

    environment {
        scannerHome = tool 'sonar-scanner'   // name of the Sonar scanner tool installed in Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'master', url: 'https://github.com/Shreyash10261/BuyMeSting'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Build Project') {
            steps {
                // allow build to continue even if prod build step fails
                sh 'npm run build || true'
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
                // bind the token stored in Jenkins credentials (id: sonar-token)
                withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                    
                    withSonarQubeEnv('LocalSonar') {
                        sh """
                        ${scannerHome}/bin/sonar-scanner \
                          -Dsonar.projectKey=BuyMeSting \
                          -Dsonar.sources=. \
                          -Dsonar.login=${SONAR_TOKEN} \
                          -Dsonar.host.url=${SONAR_HOST_URL}
                        """
                    }
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
