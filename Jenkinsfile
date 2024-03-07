pipeline {
    agent any
    environment {
        DOCKERHUB_CREDENTIALS_ID = 'DOCKERHUB_CREDENTIALS_ID'
        IMAGE_NAME = 'aaronwang0509/java'
        MAJOR_VERSION = '7'
        MINOR_VERSION = '30'
    }
    stages {
        stage('Build and Push Java 11 Image') {
            steps {
                script {
                    def imageName = "${env.IMAGE_NAME}-11"
                    def fullVersion = "${env.MAJOR_VERSION}.${env.MINOR_VERSION}.${env.BUILD_NUMBER}"
                    dir('java-11') {
                        docker.build("${imageName}:${fullVersion}")
                        docker.withRegistry('https://index.docker.io/v1/', env.DOCKERHUB_CREDENTIALS_ID) {
                            docker.image("${imageName}:${fullVersion}").push()
                        }
                    }
                }
            }
        }
        stage('Build and Push Java 17 Image') {
            steps {
                script {
                    def imageName = "${env.IMAGE_NAME}-17"
                    def fullVersion = "${env.MAJOR_VERSION}.${env.MINOR_VERSION}.${env.BUILD_NUMBER}"
                    dir('java-17') {
                        docker.build("${imageName}:${fullVersion}")
                        docker.withRegistry('https://index.docker.io/v1/', env.DOCKERHUB_CREDENTIALS_ID) {
                            docker.image("${imageName}:${fullVersion}").push()
                        }
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Build and push completed.'
        }
    }
}
