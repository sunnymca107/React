pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Docker Build & tag') {
            steps {
                sh 'docker build -t sunnymca107/react .'
                sh 'docker tag sunnymca107/react'
            }
        }
        
       
    }
}
