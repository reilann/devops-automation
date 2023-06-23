pipeline{
    agent any
    tools{
        maven 'maven'
    }
    stages{
        stage("Build Maven"){
            steps{
                 checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/owenxav/devops-automation']])
                 bat 'mvn clean install'
                }
            }
        stage('Build Docker Image'){
            steps{
                script{
                 bat 'docker build -t owenagboje/devops-integration .'
                }
            }
        }
        stage('Push Image to Docker Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhubpwd')]) {
                   sh 'docker login -u owenagboje -p ${dockerhubpwd}'
}
            }
                   sh 'docker push owenagboje/devops-integration .'
        }
        } 
    }
   }
}
