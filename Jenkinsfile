pipeline {
    agent any
    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy --version'
                sh 'uname -r'
                sh 'cat /etc/os-release'
            }
        }
        stage('dockerImageBuild'){
            steps{
                sh 'docker -v'
            }
        }
        stage('pushImage'){
            steps{
                sh 'docker images'
                sh 'docker ps'
            }
        }
    }
}