pipeline {
    agent any

    environment {
        IMAGE = "sunnymca107/react"
    
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Install') {
            steps {
                dir('react-app') {
                    sh 'npm ci'
                }
            }
        }

        stage('Build') {
            steps {
                dir('react-app') {
                    sh 'npm run build'
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t {IMAGE}:{TAG} ."
            }
        }

        stage('Push Image') {
            when {
                expression { return env.DOCKER_REGISTRY_URL }
            }
        
            }
        }
    }
}
