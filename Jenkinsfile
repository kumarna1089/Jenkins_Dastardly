pipeline {
    agent any
       
        stage ("Docker run Dastardly from Burp Suite Scan") {
            steps {
                
				@echo off

				docker pull public.ecr.aws/portswigger/dastardly:latest
	
				echo. > %WORKSPACE%\dastardly-report.xml
				
			docker run -v %WORKSPACE% -e BURP_START_URL=https://ginandjuice.shop/ -e BURP_REPORT_FILE_PATH=%WORKSPACE%\dastardly-report.xml public.ecr.aws/portswigger/dastardly:latest
            }
        }
    }
