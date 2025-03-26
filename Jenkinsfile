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
    stage('Deploy') {
        //deploy application
        docker.image('node:16-buster-slim').inside('-p 3000:3000'){
            sh './jenkins/scripts/deliver.sh'
            input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
            sh './jenkins/scripts/kill.sh'
        }
    }
}