pipeline {
    agent any

    stages {
        stage('Cleanup Workspace') {
            steps {
              sh 'rm -rf * '
            }
        }
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/RahulVarne/backend-angular.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {
                    sh '''
                        aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 545009863897.dkr.ecr.us-east-2.amazonaws.com
                        docker build -t backend:v1 . 
                        docker tag backend:v1 545009863897.dkr.ecr.us-east-2.amazonaws.com/backend:v1
                        docker push 545009863897.dkr.ecr.us-east-2.amazonaws.com/backend:v1
                        docker rmi 545009863897.dkr.ecr.us-east-2.amazonaws.com/backend:v1
                        docker rmi backend:v1
                        kubectl apply -f ./yaml/
                    '''
                }
            }
        }
    }
}
