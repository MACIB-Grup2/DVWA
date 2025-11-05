pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'SonarQube'
        SONAR_HOST_URL   = 'http://10.30.212.7:9000'
        SONAR_AUTH_TOKEN = credentials('sonarqube-token-id')
    }

    stages {
        stage('SonarQube Analysis') {
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'
                    withSonarQubeEnv("${SONARQUBE_SERVER}") {
                        sh "${scannerHome}/bin/sonar-scanner " +
                           "-Dsonar.projectKey=DVWA " +
                           "-Dsonar.sources=. " +
                           "-Dsonar.language=php " +
                           "-Dsonar.host.url=${SONAR_HOST_URL} " +
                           "-Dsonar.token=${SONAR_AUTH_TOKEN}"
                    }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                script {
                    def qg = waitForQualityGate()
                    if (qg.status != 'OK') {
                        error "Pipeline fallido: Quality Gate = ${qg.status}"
                    }
                }
            }
        }
    }
}
