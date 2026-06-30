pipeline {
    agent any

    environment {
        IMAGE = "sunnymca107/react"
        TAG = "${env.BUILD_NUMBER ?: 'latest'}"
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
                sh "docker build -t ${IMAGE}:${TAG} ."
            }
        }

        stage('Push Image') {
            when {
                expression { return env.DOCKER_REGISTRY_URL }
            }
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh "echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin ${env.DOCKER_REGISTRY_URL}"
                    sh "docker tag ${IMAGE}:${TAG} ${env.DOCKER_REGISTRY_URL}/${IMAGE}:${TAG}"
                    sh "docker push ${env.DOCKER_REGISTRY_URL}/${IMAGE}:${TAG}"
                }
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'react-app/dist/**', allowEmptyArchive: true
            cleanWs()
        }
    }
}
