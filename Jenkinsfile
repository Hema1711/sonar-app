pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'https://sonarcloud.io'
        SONAR_ORG = 'hema1711'  // Replace with your SonarCloud organization name
        SONAR_PROJECT_KEY = 'Hema1711_sonar-app' // Replace with your SonarCloud project key
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/Hema1711/sonar-app.git'  // Replace with your GitHub repo
            }
        }

        stage('Install Dependencies') {
            steps {
                script {
                    sh 'npm install'
                }
            }
        }

        stage('Build React App') {
            steps {
                script {
                    sh 'npm run build'
                }
            }
        }

        stage('Run SonarCloud Analysis') {
            steps {
                withSonarQubeEnv('SonarCloud') {
                    sh '''
                        sonar-scanner \
                        -Dsonar.projectKey=$SONAR_PROJECT_KEY \
                        -Dsonar.organization=$SONAR_ORG \
                        -Dsonar.sources=src \
                        -Dsonar.host.url=$SONAR_HOST_URL \
                        -Dsonar.login=${SONARCLOUD_TOKEN}
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
