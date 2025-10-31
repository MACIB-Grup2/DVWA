pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'SonarQube_Local'
        SONAR_HOST_URL = 'http://10.30.212.78:9000'
        SONAR_AUTH_TOKEN = credentials('sonarqube-token-id')
    }

    stages {
        stage('SonarQube Analysis') {
            steps {
                sh """
                sonar-scanner \
                    -Dsonar.projectKey=DVWA \
                    -Dsonar.sources=. \
                    -Dsonar.host.url=${SONAR_HOST_URL} \
                    -Dsonar.login=${SONAR_AUTH_TOKEN}
                """
            }
        }
    }
}
