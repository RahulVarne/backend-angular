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
    }
}
