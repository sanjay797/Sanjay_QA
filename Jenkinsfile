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
                withCredentials([gitUsernamePassword(credentialsId: 'da0c896d-f2ba-4a55-b31c-61d9f058c990', gitToolName: 'git')]) {
			
                                 sh '''#!/bin/bash -xe
				   git config --global user.name "sanjay797"
				   git config --global user.email "dhamisanjay7@gmail.com"
	                           currentDate=$(date +"%Y-%m-%d_%Hh%Mm%Ss")
				   customTagName="jenkins-${BUILD_NUMBER}--${currentDate}"
                                   git tag -a ${customTagName} -m 'Jenkinsfile push tag'
                                   git push https://${env.GIT_USERNAME}:${env.GIT_PASSWORD}@github.com/sanjay797/Sanjay_QA.git ${customTagName}
				 '''
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
