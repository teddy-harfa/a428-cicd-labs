node {
    checkout scm
    stage('Build') {
        //build application
        docker.image('node:16-buster-slim').inside('-p 3000:3000'){
            sh 'npm install'
        }
    }
    stage('Test') {
        //test application
        docker.image('node:16-buster-slim').inside('-p 3000:3000'){
            sh './jenkins/scripts/test.sh'
        }
    }
}