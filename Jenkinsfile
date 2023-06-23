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
        
   }
}
