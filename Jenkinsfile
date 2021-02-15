#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    environment {         
        VERSION = "${BUILD_ID}"        
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
                    sh 'docker tag hello-brunch:latest 10.250.12.1:5050/root/hello-brunch:BUILD-1.${VERSION}'
                    sh 'docker push 10.250.12.1:5050/root/hello-brunch:BUILD-1.${VERSION}'
                    sshagent (credentials:['gitlab-ssh']){
                        sh 'git tag BUILD-1.${VERSION}'
                        sh 'git push --tags'
                    }                    
                }                
            }
        }
        stage('Deploy') {
            steps {                
              // sh 'ssh -t deploy@10.250.12.1 'docker-compose pull & docker-compose up -d'
              sh 'ssh -t -o "StrictHostKeyChecking no" deploy@10.250.12.1 'docker-compose pull && docker-compose up -d'
            }
        }
    }
}
