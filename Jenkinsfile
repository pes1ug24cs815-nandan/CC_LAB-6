pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend Image') {
            steps {
                sh 'docker build -t backend-image ./backend'
            }
        }

        stage('Run Backend Container') {
            steps {
                sh 'docker run --name backend-container backend-image'
            }
        }

        stage('Run Nginx') {
            steps {
                sh 'docker run -d -p 9090:80 --name nginx-container nginx'
            }
        }
    }
}
