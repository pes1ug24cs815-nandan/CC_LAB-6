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
                sh '''
                docker rm -f backend-container || true
                docker run -d --name backend-container --network lab6-network backend-image
                '''
            }
        }

        stage('Run Nginx') {
            steps {
                sh '''
                docker rm -f nginx-container || true
                docker run -d -p 9090:80 \
                --name nginx-container \
                --network lab6-network \
                -v $WORKSPACE/nginx/default.conf:/etc/nginx/conf.d/default.conf \
                nginx
                '''
            }
        }
    }
}
