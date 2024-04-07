pipeline{
    agent any
    environment {
        ENV_URL = "google.com"
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
                echo "Hola world! ${ENV_URL}"
            }         
        }
        stage("third stage")
        {
            steps{
                echo "namaste world!"
            }
            
        }
    }
}