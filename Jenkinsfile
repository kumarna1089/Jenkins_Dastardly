pipeline {
    agent any
    stages {
        stage ("Docker Pull Dastardly from Burp Suite container image") {
            steps {
                sh 'docker pull public.ecr.aws/portswigger/dastardly:latest'
            }
        }
        stage ("Docker run Dastardly from Burp Suite Scan") {
            steps {
                cleanWs()
                sh 'chmod -R 777 ${WORKSPACE}'
                sh 'echo BURP_REPORT_FILE_PATH=${WORKSPACE}/dastardly-report.xml'
                sh '''
                    docker run -v ${WORKSPACE} \
                    -e BURP_START_URL=https://ginandjuice.shop/ \
                    -e BURP_REPORT_FILE_PATH=${WORKSPACE}/dastardly-report.xml \
                    public.ecr.aws/portswigger/dastardly:latest
                '''
                sh 'cat ${WORKSPACE}/dastardly-report.xml'
            }
        }
    }
    post {
        always {
            junit testResults: 'Dastdastardly-report.xml', skipPublishingChecks: true
        }
    }
}
