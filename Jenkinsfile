pipeline {
    agent any

    stages {
        stage('Pull') {
            steps {
                git branch:'main', url 'git branch: 'main', url: 'https://github.com/RahulVarne/backend-angular.git'
            }
        }
        stage('build') {
            steps {
                sh 'mvn clean package'
            }
        }
        
    }
}