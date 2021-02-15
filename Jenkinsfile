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
                withDockerRegistry([credentialsId:"gitlab-registry", url:"http://10.250.12.1:5050"]){
                    
                }
            }
        }
    }
}
