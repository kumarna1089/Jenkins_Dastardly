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
                sh '''
                    docker run --user $(id -u) --rm -v $(pwd):/dastardly -e \
                    DASTARDLY_TARGET_URL=https://ginandjuice.shop -e \
                    DASTARDLY_OUTPUT_FILE=/dastardly/dastardly-report.xml \
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
