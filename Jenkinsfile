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

    parameters {
        string(name: 'PERSON', defaultValue: 'Saurabh', description: 'Who should I say hello to?')

        text(name: 'Build Desc', defaultValue: '', description: 'Enter some information about the job')

        booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')

        choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')

        password(name: 'PASSWORD', defaultValue: 'SECRET', description: 'Enter a password')
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
                sh "sleep 1"
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