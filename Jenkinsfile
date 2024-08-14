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
                sh '''
                    docker run --user $(id -u) -v ${WORKSPACE} \
                    -e BURP_START_URL=https://ginandjuice.shop/ \
                    public.ecr.aws/portswigger/dastardly:latest
                '''
            }
        }
    }

}
