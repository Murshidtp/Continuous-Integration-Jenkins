pipeline {
    agent any 
    environment {
    DOCKERHUB_CREDENTIALS = credentials('amonkincloud-dockerhub')
    }
    stages { 

        stage('Build docker image') {
            steps {  
                sh 'docker build -t murshidtp/flaskapp:$BUILD_NUMBER .'
            }
        }   
        stage('run docker image') {
            steps {  
                sh 'docker run -d -p 3000:3000 flaskapp:$BUILD_NUMBER'
            }    
        }
        stage('login to dockerhub') {
            steps{
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        }
        stage('push image') {
            steps{
                sh 'docker push murshidtp/flaskapp:$BUILD_NUMBER'
            }
        }
}
post {
        always {
            sh 'docker logout'
        }
    }
}
