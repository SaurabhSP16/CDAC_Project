pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "saurabhsp16/my-node-app:latest"
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/saurabhsp16/https://github.com/SaurabhSP16/CDAC_Project.git'
            }
        }

        stage('Code Analysis with SonarQube') {
            steps {
                script {
                    withSonarQubeEnv('SonarQube') {
                        sh 'sonar-scanner -Dsonar.projectKey=my-app -Dsonar.sources=./src'
                    }
                }
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push Docker Image') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: 'https://index.docker.io/v1/']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name my-app $DOCKER_IMAGE'
            }
        }
    }
}

