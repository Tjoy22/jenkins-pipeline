pipeline {
    agent any
    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy fs . -o result.html'
                sh 'cat result.html'
            }
        }
        stage('dockerlogin'){
            steps{
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 796973488301.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
        stage ('dockerImageBuild'){
            steps{
                sh 'docker build -t jenkins-ci .'
                sh 'docker build -t imageversion .'
            }
        }
        stage ('dockerImageTag'){
            steps{
                sh 'docker tag jenkins-ci:latest 796973488301.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:latest'
                sh 'docker tag imageversion 796973488301.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:V1.$BUILD_NUMBER'
            }
        }
        stage('pushImage'){
            steps{
                sh 
                sh docke'r push 796973488301.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci:V1.$BUILD_NUMBER'
            }

        }
    }
}