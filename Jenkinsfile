pipeline {
    agent any

    stages {
        stage('SonarQube Analysis') {
            steps {
                script {
                    docker.image('sonarqube/sonar-scanner-cli:5.0.1')
                           .inside("-u root -v ${WORKSPACE}:/usr/src") {
                        withSonarQubeEnv('SonarQube') {
                            sh '''
                                cd /usr/src
                                sonar-scanner \
                                    -Dsonar.projectKey=DVWA \
                                    -Dsonar.sources=.
                            '''
                        }
                    }
                }
            }
        }
    }
}
