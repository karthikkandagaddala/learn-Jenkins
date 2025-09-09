pipeline {
    agent {
        label 'karthik-agent-1'
    }
    options {
        timeout(time: 30, unit: 'MINUTES') //This is for with in timeout purpose wwe will use 
        disableConcurrentBuilds() //This is for at a time couldnt run multiple jobs or pipelines
        ansiColor('xterm')
    }
    environment {
        DEPLOY_TO = 'production'
        GREETING = 'Good Morning'  
    }
    stages {
        stage('build') {
            steps {
                sh 'echo this is build'
                sh 'env'
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
    }
    post {
        always {
            echo 'previous workspace files will get delete beacuse next any changes happen means it wont update'
            deleteDir()
        }
        success {
            echo 'Pipeline is success, then only it will run'
        }
        failure {
            echo 'Pipeline is failure, then only it will run'
        }
    }
}