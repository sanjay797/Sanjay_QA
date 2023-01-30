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
                withCredentials([gitUsernamePassword(credentialsId: 'ce0d7a9d-3f28-425e-a936-8bca271d991f', gitToolName: 'git')]) {
			sh("git config --global --unset http.proxy")
			sh("git config --global --unset https.proxy")

                sh("git tag -a some_tag_3 -m 'Jenkins'")
		sh("git push https://${env.GIT_USERNAME}:${env.GIT_PASSWORD}@https://github.com/sanjay797/Sanjay_QA.git --tags")
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
