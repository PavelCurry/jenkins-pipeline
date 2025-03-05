pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-1'
        ECR_REPO ='536697238312.dkr.ecr.us-east-1.amazonaws.com'
        IMAGE_ECR_REPO ='536697238312.dkr.ecr.us-east-1.amazonaws.com/dev'
    }
    stages{
        stage('CodeScan'){
            steps{
                sh 'trivy fs .  -o result.html'
                sh 'cat result.html'
                
            }
        }
        stage('dockerLogin)'){
            steps{
                sh 'aws ecr get-login-password --region $AWS_REGION | docker login --username AWS --password-stdin $ECR_REPO'
            }
        }
        stage('dockerImageBuild'){
            steps{
                sh 'docker build -t dev . '
                sh 'docker build -t imageversions . '
            }
        }
        stage(DockerTag){
            steps{
                sh 'docker tag dev:latest $ECR_REPO/dev:latest'
                sh 'docker tag imageversions $IMAGE_ECR_REPO:v1.$BUILD_NUMBER'
            }
        }
        stage(DockerPush){
            steps{
                sh 'docker push $IMAGE_ECR_REPO:latest'
                sh 'docker push $IMAGE_ECR_REPO:v1.$BUILD_NUMBER'
            }
        }
       
    }
}