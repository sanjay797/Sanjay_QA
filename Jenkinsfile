pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo "Hello world"
                echo "sanjay"
<<<<<<< HEAD
                echo "dhami"
=======
>>>>>>> 5addae9c7d16d08faa96ad66dbede241a06d9bfd
                
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
