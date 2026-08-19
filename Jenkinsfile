pipeline {
    agent { 
         docker {
               image 'node:22-alpine'
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
        stage('Deliver for Deployment') { 
            when {
                branch 'development'
            }
            steps { 
                sh './jenkins/scripts/deliver-for-development.sh'
                input  message:'Finish using the web site? (Click "Proceed" to continue)'
                sh './jenkins/script/kill.sh'
            }
        }
        stage('Deliver for production') { 
            when {
                branch 'production'
            }
            steps { 
                sh './jenkins/scripts/deploy-for-production.sh'
                input  message:'Finish using the web site? (Click "Proceed" to continue)'
                sh './jenkins/script/kill.sh'
            }
        }
    }
}
