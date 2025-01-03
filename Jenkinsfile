pipeline {
    agent any
    tools {
        nodejs 'nodejs-20.11.0' // Name of the Node.js installation in Jenkins
    }

    environment {
        NODEJS_HOME = 'C:/Program Files/nodejs'  // Set the Node.js path
        SONAR_SCANNER_PATH = 'D:/altered/sonar-scanner-6.2.1.4610-windows-x64/bin'
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
