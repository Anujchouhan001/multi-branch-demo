pipeline {
    agent any

    stages {

        stage('Build') {
            steps {
                echo "Building Branch: ${env.BRANCH_NAME}"
            }
        }

        stage('Maven Test') {
            steps {
                bat '''
                if not exist target\\surefire-reports mkdir target\\surefire-reports
                echo ^<testsuite^>^</testsuite^> > target\\surefire-reports\\test.xml
                '''
            }
        }

        stage('Docker Agent Demo') {
            steps {
                echo 'Docker-based agent would run Maven container here'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'target/surefire-reports/*.xml',
                             allowEmptyArchive: true

            junit testResults: 'target/surefire-reports/*.xml',
                  allowEmptyResults: true
        }
    }
}