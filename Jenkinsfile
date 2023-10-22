pipeline {
    environment {
        registry = "skandersoltane/simple-app"
        registryCredential = 'dckr_pat_iTj37v7dE4n0_IG1vzZySi33EY8'
        dockerImage = 'simple-app'
    }
    agent any
    stages {
        stage('Cloning our Git') {
            steps {
                git 'https://github.com/LetMePy/obitemservice.git'
            }
        }
        stage('Building our image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
        stage('Cleaning up') {
            steps {
                sh "docker rmi $registry:$BUILD_NUMBER"
            }
        }
    }
}

