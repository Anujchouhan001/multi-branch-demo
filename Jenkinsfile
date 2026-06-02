pipeline {
    agent {
        docker {
            image 'maven:3.9.6-eclipse-temurin-17'
        }
    }

    stages {

        stage('Build') {
            steps {
                echo "Building Branch: ${env.BRANCH_NAME}"
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
    }

    post {
        always {

            junit '**/target/surefire-reports/*.xml'

            archiveArtifacts artifacts:
                '**/target/surefire-reports/*.xml',
                fingerprint: true
        }
    }
}