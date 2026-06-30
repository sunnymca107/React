pipeline {
    agent any
    triggers{
        cron '*/20 * * * *'
    }
    stages {
        stage('clone') {
            steps {
		git branch: 'main', url: 'https://github.com/Aakash0706/2nd-ia-devops.git'
            }
        }
        stage('Build') {
            steps {
                sh 'npm install'
                sh 'npm run build'
            }
        }
        stage('Docker Build & tag') {
            steps {
                sh 'docker build -t 2nd-ia .'
                sh 'docker tag 2nd-ia sunnymca107-ia'
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
                        docker push sunnymca107-ia:latest
                        '''
                    }
            }
        }
        
        stage('pull and run') {
            steps {
                sh 'docker pull jaiswalakash/2nd-ia'
		 sh 'docker rm -f 2nd-ia || true'
                sh 'docker run -d -p 9092:80 jaiswalakash/2nd-ia'
            }
        }
    }
}
