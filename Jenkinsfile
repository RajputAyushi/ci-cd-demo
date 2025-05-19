pipeline {
    agent any

    environment {
        IMAGE_NAME = "ci-cd-demo"
    }

    stages {
        stage('Checkout') {
            steps {

                git 'https://github.com/RajputAyushi/ci-cd-demo.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Docker Build') {
            steps {
                script {
                    docker.build("${IMAGE_NAME}")
                }
            }
        }
 stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('', 'docker-hub-creds') {
                        docker.image("${IMAGE_NAME}").push()
                    }
                }
            }

        }
        stage('Notify') {
            steps {
                echo 'You can add Slack/email notification here.'
            }
        }
    }
}
