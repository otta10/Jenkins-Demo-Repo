pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                checkout scmGit(branches: [[name: '*/master']], extensions: [], 
                userRemoteConfigs: [[url: 'https://github.com/otta10/Jenkins-Demo-Repo.git']])
            }
        }
        
        stage('Build with Maven') {
            steps {
                sh 'cd MySampleWebApp && mvn clean install'
            }
        }
        
        stage('Test') {
            steps {
                sh 'cd MySampleWebApp && mvn test'
            }
        }
        
        stage('Deploy to Tomcat') {
            steps {
                deploy adapters: [tomcat9(credentialsId: 'b3f06ebe-3c1f-483c-8648-3b5247846d43', path: '', 
                url: 'http://54.202.148.112:8080/')], 
                contextPath: 'webapp', war: '**/*.war'
            }
        }
    }
}

