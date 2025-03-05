pipeline {
    agent any
    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy fs .  -o result.html'
                sh 'cat result.html'
                
            }
        }
        stage('dockerLogin)'){
            steps{
                sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 536697238312.dkr.ecr.us-east-1.amazonaws.com'
            }
        }
        stage('dockerImageBuild'){
            steps{
                sh 'docker build -t dev . '
                sh 'docker build -t imageversion . '
            }
        }
        stage(DockerTag){
            steps{
                sh 'docker tag dev:latest 536697238312.dkr.ecr.us-east-1.amazonaws.com/dev:latest'
                sh 'docker tag imageversion:latest 536697238312.dkr.ecr.us-east-1.amazonaws.com/imageversion:v1.$BUILD_NUMBER'
            }
        }
        stage(DockerPush){
            steps{
                sh 'docker push 536697238312.dkr.ecr.us-east-1.amazonaws.com/dev:latest'
                sh 'docker push 536697238312.dkr.ecr.us-east-1.amazonaws.com/dev:v1.$BUILD_NUMBER'
            }
        }
       
    }
}