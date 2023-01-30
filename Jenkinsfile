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
	  withCredentials([gitUsernamePassword(credentialsId: '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', gitToolName: 'git')]) {
	       //        sh '''#!/bin/bash -xe
		   sh "echo "ram1""
		   sh currentDate=$(date +"%Y-%m-%d_%Hh%Mm%Ss")
		   sh customTagName="jenkins-${BUILD_NUMBER}--${currentDate}"
		   sh "echo "ram""
                   sh "git tag -a ${customTagName} -m 'Jenkinsfile push tag'"
                   sh "git push https://${env.GIT_USERNAME}:${env.GIT_PASSWORD}@https://github.com/sanjay797/Sanjay_QA.git ${customTagName}"
		 //    '''
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
