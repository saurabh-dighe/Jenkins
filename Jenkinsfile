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
                sh "echo hello world! ${ENV_URL}"
  //              sh "${env}"
            }
            
        }
        stage("second stage")
        {
            environment {
                ENV_URL = "facebook.com"
            }
            steps{
                sh "echo ${ENV_URL}"
            //    sh "CRED"
            }         
        }
        stage("third stage")
        {
            steps{
                sh "env"
            }
            
        }
    }
}