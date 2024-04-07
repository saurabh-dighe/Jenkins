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
                sh "${env}"
            }
            
        }
        stage("second stage")
        {
            steps{
                echo "Hola world!"
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