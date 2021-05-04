pipeline {
    agent any

    stages {
        stage('Test') {
            steps {
                echo 'Testing..'
		sh 'npm install'
		sh 'npm test'
            }
        }
        
    }
	post { 
        	always { 
            		echo 'Pipeline finished!'
        }
		failure {
			echo 'Testing failed!'
        		mail to: 'michalpast034@gmail.com',
             			subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             			body: "Something is wrong with ${env.BUILD_URL}"
    	}
		success {
			echo 'Testing successful!'
        		mail to: 'michalpast034@gmail.com',
             			subject: "Successful Pipeline: ${currentBuild.fullDisplayName}",
             			body: "Everything worked fine"
    	}
    }
}