pipeline {
    agent any

    stages {
        stage('Cleanup Workspace') {
            steps {
                deleteDir() // Deletes all files in the workspace
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
        stage('deploy') {
            steps {
                sh '''
                    docker build -t backend . 
                    docker tag backend:latest 545009863897.dkr.ecr.us-east-2.amazonaws.com/backend:latest
                    docker push 545009863897.dkr.ecr.us-east-2.amazonaws.com/backend:latest
                    docker rmi 545009863897.dkr.ecr.us-east-2.amazonaws.com/backend:latest
                    docker rmi backend
                 // kubectl apply -f ./yaml/ 
                 '''
            }
        }
    }
}
