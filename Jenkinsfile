pipeline {
    agent {
        docker {
            image 'node:lts-buster-slim'
            args '-p 3000:3000'
        }
    }
    stages {
        stage('Build') {
            steps {
               
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh "chmod +x -R ${env.WORKSPACE}"
                sh './jenkins/test.sh'
            }
        }
        stage('Deliver') { 
            steps {
                sh './jenkins/deliver.sh' 
                input message: 'Finished using the web site? (Click "Proceed" to continue)' 
                sh './jenkins/kill.sh' 
            }
        }
    }
}