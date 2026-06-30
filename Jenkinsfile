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
        
        stage('Docker push') {
            steps {
               withCredentials([usernamePassword(
                    credentialsId: "Dockerfile",
                    usernameVariable: 'USER', 
                    passwordVariable: 'PASS'
                    )]) {
                        sh '''
                        echo $PASS | docker login -u $USER --password-stdin
                        docker push sunnymca107/react:latest
                        '''
                    }
            }
        }
        
        stage('pull and run') {
            steps {
                sh 'docker pull sunnymca107/react'
		 sh 'docker rm sunnymca107/react || true'
                sh 'docker run -d -p 9092:80 sunnymca107/react'
            }
        }
    }
}
