pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo "Hello world"
                echo "sanjay"
                echo "rohan"
		echo "kunal"
		echo "kunal1"
                
                    }
            }
	 stage('get_commit_msg') {
            steps {
        	script {
            		env.GIT_COMMIT_MSG = sh (script: 'git log -1 --pretty=%B ${GIT_COMMIT}', returnStdout: true).trim()
			echo "${GIT_COMMIT_MSG}"
        }
    }
}
     }
   post {

        always {

            allure includeProperties: false, jdk: '', results: [[path: 'test/acceptance/report']]
            
			
	    emailext to: "dhamisanjay7@gmail.com",
            subject: "jenkins build:${currentBuild.currentResult}: ${env.JOB_NAME}",
            body: "${currentBuild.currentResult}: Job ${env.JOB_NAME}\nMore Info can be found here: ${env.BUILD_URL}allure\n Commit log - ${GIT_COMMIT_MSG}"
                
                
           
			

    }
}
}
