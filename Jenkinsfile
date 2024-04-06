pipeline{
    agent any

    stages{
        stage("first stage")
        {
            steps{
                echo "hello world!"
            }
            
        }
        stage("second stage")
        {
            steps{
                echos "Hola world!"
                exit 0
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