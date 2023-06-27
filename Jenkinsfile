pipeline {
    agent {
        docker {
            image 'node:16-buster-slim'
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
                sh './jenkins/scripts/test.sh' 
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy?', submitter: 'user', submitterParameter: 'proceed'
            }
        }
        stage('Deploy') {
            steps {
                // Langkah-langkah untuk deploy aplikasi React
                sh './jenkins/scripts/deliver.sh'
                sh './jenkins/scripts/kill.sh'
                
                // Tunggu selama 1 menit sebelum melanjutkan
                sleep time: 1, unit: 'MINUTES'
            }
        }
    }
}
