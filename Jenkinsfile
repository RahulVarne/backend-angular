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
        stage('Deploy') {
            steps {
                withCredentials([[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    credentialsId: 'aws-credentials'
                ]]) {
                    sh '''
                        aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 545009863897.dkr.ecr.us-east-2.amazonaws.com
                        docker build -t backend . 
                        docker tag backend:latest 545009863897.dkr.ecr.us-east-2.amazonaws.com/backend:latest
                        docker push 545009863897.dkr.ecr.us-east-2.amazonaws.com/backend:latest
                        docker rmi 545009863897.dkr.ecr.us-east-2.amazonaws.com/backend:latest
                        docker rmi backend
                        # kubectl apply -f ./yaml/
                    '''
                }
            }
        }
    }
}
