pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'https://sonarcloud.io'
        SONAR_ORG = 'Hema1711'  // Replace with your SonarCloud organization name
        SONAR_PROJECT_KEY = 'Hema1711_sonar-app' // Replace with your SonarCloud project key
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/Hema1711/sonar-app.git'  // Replace with your GitHub repo
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'npm install'
            }
        }

        stage('Build React App') {
            steps {
                bat 'npm run build'
            }
        }

        stage('Run SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    bat '''
                        sonar-scanner ^
                        -Dsonar.projectKey=%SONAR_PROJECT_KEY% ^
                        -Dsonar.organization=%SONAR_ORG% ^
                        -Dsonar.sources=src ^
                        -Dsonar.host.url=%SONAR_HOST_URL% ^
                        -Dsonar.login=%SONARCLOUD_TOKEN%
                    '''
                }
            }
        }

        stage('Deploy') {
            steps {
                echo "Deployment Step (You can add deployment commands here)"
            }
        }
    }
}
