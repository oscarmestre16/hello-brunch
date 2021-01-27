
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
        stage('deploy') {
            steps {
                sh 'docker-compose up -d'
            }
        }
    }
}
