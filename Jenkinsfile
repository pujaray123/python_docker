pipeline {
    agent any

    environment{
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker build -t pujaray/python-doc-jenkins .'
                echo 'Building..'
            }
        }
        stage('Login') {
            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
                echo 'Login in to dockerhub..'
            }
        }
        stage('Push') {
            steps {
                sh 'docker push pujaray/python-doc-jenkins'
                echo 'pushing..'
            }
        }
        post {
            always {
                sh 'docker logout'
            }
        }
    }
}