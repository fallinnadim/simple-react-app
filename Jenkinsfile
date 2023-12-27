node {
    properties([pipelineTriggers([pollSCM('TZ=Asia/Jakarta\nH/2 * * * *')])])
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {
        stage('Build') {
            sh 'npm install'
        }
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Manual Approval') {
            input message: 'Lanjut ke tahap Deploy? (Klik "Proceed" untuk mengakhiri)' 
        }
        stage('Deploy') {
            sh './jenkins/scripts/deliver.sh'
        }
    }
}