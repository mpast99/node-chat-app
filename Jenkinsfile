pipeline {
    agent any

    stages {
	stage('Build') {
            steps {
                echo 'Building..'
		sh 'git pull'
		sh 'npm install'
            }
	    post { 
		failure {
			echo 'Building failed!'
			currentBuild.result = 'ABORTED'
			emailext attachLog: true,
                		subject: "Failed Building: ${currentBuild.fullDisplayName}",
             			body: "${env.BUILD_URL} failed at building stage",
                		recipientProviders: [developers(), requestor()],
                		to: 'michalpast034@gmail.com'
             			
    	}
		success {
			echo 'Building successful!'
			emailext attachLog: true,
                		subject: "Successful Building: ${currentBuild.fullDisplayName}",
             			body: "Building worked fine",
                		recipientProviders: [developers(), requestor()],
                		to: 'michalpast034@gmail.com'
    	}
    }
        }
        stage('Test') {
	    when {
        expression { currentBuild.result == 'SUCCESS' }
      
            steps {
                echo 'Testing..'
		sh 'npm test'
            }
        }
        
    }
}
	post { 
        	always { 
            		echo 'Pipeline finished!'
        }
		failure {
			echo 'Testing failed!'
			emailext attachLog: true,
                		subject: "Failed Pipeline: ${currentBuild.fullDisplayName}",
             			body: "Something is wrong with ${env.BUILD_URL}",
                		recipientProviders: [developers(), requestor()],
                		to: 'michalpast034@gmail.com'
             			
    	}
		success {
			echo 'Testing successful!'
			emailext attachLog: true,
                		subject: "Successful Pipeline: ${currentBuild.fullDisplayName}",
             			body: "Everything worked fine",
                		recipientProviders: [developers(), requestor()],
                		to: 'michalpast034@gmail.com'
    	}
    }
}