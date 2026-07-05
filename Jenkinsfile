pipeline {
    agent any

    tools {
        jdk 'JDK21'
        maven 'Maven'
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'git',
                    url: 'git@github.com:swapnil19082024/devops-java-app.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-java-app:v1 .'
            }
        }

        stage('Deploy Container') {
            steps {
                sh '''
                docker rm -f devops-app || true
                docker run -d --name devops-app -p 8081:8080 devops-java-app:v1
                '''
            }
        }
    }
} 
