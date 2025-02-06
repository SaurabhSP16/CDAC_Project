pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/SaurabhSP16/CDAC_Project.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t youtube .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 3000:3000 --name ditiss youtube'
            }
        }
    }
}

