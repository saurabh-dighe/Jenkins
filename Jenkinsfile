pipeline{
    agent any
    environment {
        ENV-URL = "google.com"
    }
    stages{
        stage("first stage")
        {
            steps{
                sh "echo hello world! ${ENV-URL} "
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