pipeline{
    agent any{
        stages{
            stage('build docker image'){
                steps{
                    sh'docker build -t sunnymca107/react '
                }
            }
            stage('push docker image to docker hub'){
                steps{
                    sh 'echo "password" / docker login -u '
                }
            }
            stage
        }       
    }
}