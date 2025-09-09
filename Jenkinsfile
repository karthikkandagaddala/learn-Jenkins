pipeline {
    agent {
        label 'karthik-agent-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES') //This is for with in timeout purpose wwe will use 
        disableConcurrentBuilds() //This is for at a time couldnt run multiple jobs or pipelines
    }
    stages {
        stage('build') {
            steps {
                sh 'echo this is build'
            }
        }
        stage('test') {
            steps {
                sh 'echo this is test'
            }
        }
        stage('deploy') {
            steps {
                sh 'echo this is deploy'
            }
        }
        stage('karthik') {
            steps {
                sh 'echo Hi I am karthik'
            }
        }
        stage('DCB') {
            steps {
                sh 'echo offer in DCB'
            }
        }
    }
}