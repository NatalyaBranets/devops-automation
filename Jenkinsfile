pipeline {
    agent any
    tools{
        maven 'maven_3_9_8'
    }
    stages{
        stage('Build Maven') {
            steps{
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/NatalyaBranets/devops-automation']])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image') {
            steps{
                script{
                    sh 'docker build -t nbranets/devops-automation .'
                }
            }
        }
        stage('Push docker image to DockerHub') {
            steps{
                script{
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                    sh 'docker login -u nbranets567@gmail.com -p ${dockerhubpwd}'

    }
                    sh 'docker push nbranets/devops-automation'
                }
            }
        }
    }
}