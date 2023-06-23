pipeline{
    agent any
    tools{
        maven 'maven'
    }
    environment {
    DOCKERHUB_CREDENTIALS = credentials('docker-hub-owenagboje')
    }
    stages{
        stage("SCM Checkout"){
            steps{
                 checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/owenxav/devops-automation']])
            }
        }
        stage("maven Build"){
            steps{
                bat 'mvn clean install'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                 bat 'docker build -t owenagboje/devops-integration .'
                }
            }
        }
        stage('Push image to Hub'){
            steps{
                script{
                   withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                   bat 'docker login -u owenagboje -p ${dockerhubpwd}'

}
                   bat 'docker push owenagboje/devops-integration'
                }
            }
        }
        stage('Deploy to k8s'){
            steps{
                script{
                    kubernetesDeploy (configs: 'deploymentservice.yaml',kubeconfigId: 'k8sconfigpwd')
                }
            }
        }
    }
}
