pipeline {
    agent any
    stages {
        stage ("Docker Pull Dastardly from Burp Suite container image") {
            steps {
                bat 'docker pull public.ecr.aws/portswigger/dastardly:latest'
            }
        }
        
        stage ("Docker run Dastardly from Burp Suite Scan") {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE')
                {
                bat '''
                    docker run -v ${WORKSPACE} \
                    -e BURP_START_URL=https://ginandjuice.shop/ \
                    -e BURP_REPORT_FILE_PATH=${WORKSPACE}\\dastardly-report.xml \
                    public.ecr.aws/portswigger/dastardly:latest
                '''
            }
            }
        }
    }
}
