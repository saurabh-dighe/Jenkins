pipeline{
    agent any
    environment {
        ENV_URL = "google.com"
        CRED =credentials('SSH-CRED')
    }
    stages{
        stage("first stage")
        {
            steps{
                sh "echo ${ENV_URL}"
                sh 'echo "User is $CRED_USR"'
            }            
        }
        stage("second stage")
        {
            steps{
                sh "env"
            } 
        }
    }
}