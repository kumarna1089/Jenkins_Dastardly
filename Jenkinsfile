pipeline {
    agent any
    stages {
        stage ("Docker Pull Dastardly from Burp Suite container image") {
            steps {
                powershell 'docker pull public.ecr.aws/portswigger/dastardly:latest'
            }
        }
        stage ("Docker run Dastardly from Burp Suite Scan") {
            steps {
                cleanWs()
                powershell 'chmod -R 777 ${WORKSPACE}'
                powershell 'echo $env:BURP_REPORT_FILE_PATH="${WORKSPACE}\\dastardly-report.xml"'
                powershell '''
                    docker run -v ${WORKSPACE}:${WORKSPACE}:rw \
                    -e BURP_START_URL=https://ginandjuice.shop/ \
                    -e BURP_REPORT_FILE_PATH=$env:BURP_REPORT_FILE_PATH \
                    public.ecr.aws/portswigger/dastardly:latest
                '''
            }
        }
    }
    post {
        always {
            junit testResults: 'dastardly-report.xml', skipPublishingChecks: true
        }
    }
}
