#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    environment { 
        
        VERSION = "${env.BUILD_ID}-${env.GIT_COMMIT}"
        
    }
    stages {
        stage('Build') {
            steps {                
                sh 'docker-compose build'
            }
        }
        stage('Publish') {
            steps {
                              
                withDockerRegistry([credentialsId:"gitlab-registry", url:"http://10.250.12.1:5050"]){
                    sh 'docker tag hello-brunch:latest 10.250.12.1:5050/root/hello-brunch:latest ${VERSION}'
                    sh 'docker push 10.250.12.1:5050/root/hello-brunch:latest ${VERSION}'
                }
            }
        }
    }
}
