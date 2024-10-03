pipeline {
    agent any 
    tools {
        maven 'maven 3.9.9'
    }
    stages {
        stage('Build Maven'){
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/amit---kumar/userservice']])
                sh 'echo hello'
                sh 'echo $USER'
                sh 'mvn clean install'
                
            }
            
        }
        stage('Build docker image') {
            steps {
                script {
                    sh 'docker build -t dockaas20/user-service .'
                }
            }
        }
        stage('Push image to Hub') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'dockerhubpwd2', variable: 'dockerhubpwd2')]) {
                        sh 'docker login -u dockaas20 -p ${dockerhubpwd2}' 
                    }
                    sh 'docker push dockaas20/user-service'
                }
            }
        }
    }
}
