pipeline {
    agent any
    stages {
        stage('Preparation') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/bayader93/project.git'
            }
        }
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                withCredentials([usernamePassword(credentialsId:"test",usernameVariable:"username",passwordVariable:"pass")]){
                sh 'docker build . -t ${username}/nodejs:v1.0'
                sh 'docker login -u ${username} -p ${pass}'
                sh 'docker push ${username}/nodejs:v1.0'
                }
            }
        }  
        
        stage('Push Docker Images to Nexus Registry'){
             steps{
             sh 'docker login -u user -p password https://nexus3.onap.org/repository/nodejs/'
             sh 'docker push https://nexus3.onap.org/repository/nodejs//nodejs:v1.0}'
             }
          }
    }
}