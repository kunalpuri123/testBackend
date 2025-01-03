pipeline {
    agent any
    tools {
        nodejs 'nodejs-20.11.0' // Name of the Node.js installation in Jenkins
    }

    environment {
        NODEJS_HOME = '/Users/kunalpuri/.nvm/versions/node/v22.9.0/bin/node'  // Set the Node.js path
        SONAR_SCANNER_PATH = '/opt/homebrew/bin/sonar-scannern'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code for all repositories
                checkout scm
            }
        }


        stage('Install Dependencies - Backend') {
            steps {
                
                    bat '''
                    set PATH=%NODEJS_HOME%;%PATH%
                    npm install
                    '''
                
            }
        }

    

        stage('SonarQube Analysis - Backend 1') {
            environment {
                SONAR_TOKEN = credentials('sonar-token')
            }
            steps {
               
                    bat '''
                    D:/altered/sonar-scanner-6.2.1.4610-windows-x64/bin/sonar-scanner.bat -Dsonar.projectKey=new-backend ^
                        -Dsonar.sources=. ^
                        -Dsonar.host.url=http://localhost:9000 ^
                        -Dsonar.token=%SONAR_TOKEN%
                    '''
                }
            
        }

    }    

    post {
        success {
            echo 'Pipeline completed successfully for all components.'
        }
        failure {
            echo 'Pipeline failed for one or more components.'
        }
        always {
            echo 'This runs regardless of the result.'
        }
    }
}
