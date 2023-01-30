pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo "Hello world"
                echo "sanjay"
                echo "rohan"
                
                    }
            }
	   stage('git tagging') {
            steps {
                sh '''#!/bin/bash -xe
                 currentDate=$(date +"%Y-%m-%d_%Hh%Mm%Ss")
                 customTagName="jenkins-${BUILD_NUMBER}--${currentDate}"
	        echo CUSTOM_TAG_NAME=${customTagName} >> ${PROPERTIES_FILE_NAME}
               '''
	  
	  script {
         def PROPERTIES = readProperties file: "${PROPERTIES_FILE_NAME}"
         env.CUSTOM_TAG_NAME = PROPERTIES.CUSTOM_TAG_NAME
     }
	 
      withCredentials([gitUsernamePassword(credentialsId: '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', gitToolName: 'git')]) {
                sh "git tag -a ${CUSTOM_TAG_NAME} -m 'Jenkinsfile push tag'"
                sh("git push https://${env.GIT_USERNAME}:${env.GIT_PASSWORD}@github.com/sanjay797/Sanjay_QA.git ${CUSTOM_TAG_NAME}")
              } 
           }
        }
     }
   post {

        always {

            allure includeProperties: false, jdk: '', results: [[path: 'test/acceptance/report']]
            
			
			emailext to: "dhamisanjay7@gmail.com",
            subject: "jenkins build:${currentBuild.currentResult}: ${env.JOB_NAME}",
            body: "${currentBuild.currentResult}: Job ${env.JOB_NAME}\nMore Info can be found here: ${env.BUILD_URL}allure"
                
                
           
			

    }
}
}
