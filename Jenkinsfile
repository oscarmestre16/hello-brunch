#!/usr/bin/env groovy
pipeline {
    agent any
    options {
        ansiColor('xterm')
    }
    stages {
        stage('Build') {
            steps {
                //Rama main y no master
               // git url: 'https://github.com/oscarmestre16/hello-brunch.git', branch:'main'
                sh 'docker-compose build'
            }
        }
        stage('Publish') {
            steps {
                withDockerRegistry([credentialsId:"jenkins-publish", url:"http://10.250.12.1:5050"]){
                    sh 'docker tag hello-brunch:latest 10.250.12.1:5050/root/hello-brunch:latest'
                    sh 'docker push 10.250.12.1.5050/root/hello-brunch:latest'
                }
            }
        }
    }
}
