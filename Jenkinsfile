pipeline {
    agent any
    environment {
        USERNAME_PASSWORD = credentials('dockerhub-madhu')
    }
    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/code-with-madhu/python-flask-docker-app.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t ${USERNAME_PASSWORD_USR}/simple-flask-app:latest .'
            }
        }
        stage('Run Docker Container') {
            steps {
                sh 'docker run -d -p 5000:5000 ${USERNAME_PASSWORD_USR}/simple-flask-app:latest'
            }
        }
        stage('Docker Image Publish') {
            steps {
                sh "docker login -u ${USERNAME_PASSWORD_USR} -p ${USERNAME_PASSWORD_PSW}"
                sh "docker push ${USERNAME_PASSWORD_USR}/simple-flask-app:latest"
            }
        }
    }
}
