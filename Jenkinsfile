pipeline {
    agent { 
         docker {
               image 'node:6-alpine'
	       args '-p 3000:3000 -p 5000:5000'
	 }
    }
    environment {
        CI = 'true'
    }


    stages {
        stage('Build') {
            steps {
	      echo 'Setup npm install...'
               sh 'npm install'
            }
        }
	stage('Test') {
               steps {
	          echo 'Running test scripts...'
                   sh './jenkins/scripts/test.sh'
	       }
	}
    }
}
