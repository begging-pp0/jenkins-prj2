pipeline {
    agent any
    tools {
        maven ''mvn3
    }
    
    environment {
      TOMCAT_IP = "3.85.195.227"
    }
    
    stages {
        stage('Hello'){
            steps{
                echo 'Say hello first...'
            }
        }
        
        stage('checkout'){
            steps{
                checkout scmGit(branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/begging-pp0/jenkins-prj2.git']])
            }
        }
        
        stage('Build'){
            steps{
                echo 'Building Maven Project'
                sh 'mvn clean install'
            }
        }
        
        stage('Deploy on Tomcat'){
            steps{
                echo 'Deploying on Tomcat'
                sshagent(['tomcat-key']){
                    sh 'scp -v -o StrictHostKeyChecking=no target/demowar-0.0.1-SNAPSHOT.war ubuntu@$TOMCAT_IP:/opt/tomcat/webapps'
                }
            }
        }
        
    }
    
}



