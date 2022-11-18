pipeline {
    agent any
    tools {
        maven "maven_3_8_6"
    }
    stages {
        stage('Build Maven') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ShamilkaG/devops-automation']]])
                bat 'mvn clean install'
            }
        }
        stage('Build Docker image'){
            steps{
                script{
                    bat 'docker build -t shamilka/devops-integration .'
                }
            }
        }
        stage('Push image to hub'){
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dcker_pwd')]) {
                    bat 'docker login -u shamilka -p %dcker_pwd%'
}
                    bat 'docker push shamilka/devops-integration'
                }
            }
        }

    }
}