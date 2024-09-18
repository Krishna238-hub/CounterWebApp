pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                git 'https://github.com/rameshkalluri/CounterWebApp.git'
            }
        }
        stage('build') {
            steps {
                bat 'mvn clean install'
            }
        }
        stage('Docker build') {
            steps {
                bat 'docker build -t cw .'
            }
        }      
        stage('Docker tag') {
            steps {
                bat 'docker tag  cw:latest rrksrb/cw:1'
            }
        }      
        stage('publish to registry') {
            steps{
                withDockerRegistry(credentialsId: 'docker', url: 'https://registry.hub.docker.com') {
                   bat 'docker push rrksrb/cw:1'
                }
            }
        }
    }
}
