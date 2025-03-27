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
    stage('Manual Approval') {
        //approve deploy application
        input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk melakukan approve)'
    }
    stage('Deploy') {
        //deploy application
        docker.image('node:16-buster-slim').inside('-p 3000:3000'){
            sh './jenkins/scripts/deliver.sh'
            //biarkan aplikasi berjalan 1 menit
            sleep time: 1, unit: 'MINUTES'
            //stop aplikasi setelah berjalan 1 menit
            sh './jenkins/scripts/kill.sh'
        }
    }
}