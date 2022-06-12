pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage('Build Maven'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Java-Techie-jt/devops-automation']]])
                sh 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t minhnhatict/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-minhnhatict-pwd', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u minhnhatict -p ${dockerhubpwd}' 
}
                    
                   sh 'docker push minhnhatict/devops-integration'
                }
            }
        }
    }
}
