pipeline{
    agent any
    environment {
        ENV_URL = "google.com"
        CRED =credentials('SSH-CRED')
    }
    options{
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'MINUTES')
    }
    stages{
        stage("first stage")
        {
            steps{
                sh "echo $ENV_URL"
                sh "echo User is $CRED_USR"
            }            
        }
        stage("second stage")
        {
            steps{
                sh "env"
                sh "sleep 120"
            } 
        }
        stage("third stage")
        {
            steps{
                sh "echo Hii"
            } 
        }        
    }
}