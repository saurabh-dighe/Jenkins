pipeline{
    agent {label 'ws'}
    environment {
        ENV_URL = "google.com"
        CRED =credentials('SSH-CRED')
    }
    options{
        buildDiscarder(logRotator(numToKeepStr: '10'))
        disableConcurrentBuilds()
        timeout(time: 1, unit: 'MINUTES')
    }

    // parameters {
    //     string(name: 'PERSON', defaultValue: 'Saurabh', description: 'Who should I say hello to?')
    //     text(name: 'Build Desc', defaultValue: '', description: 'Enter some information about the job')
    //     booleanParam(name: 'TOGGLE', defaultValue: true, description: 'Toggle this value')
    //     choice(name: 'CHOICE', choices: ['One', 'Two', 'Three'], description: 'Pick something')
    // }

    tools{
        maven 'mvn-390'
    }
    triggers {
//        cron ('*/1 * * * *')
          pollSCM ('*/1 * * * *')
        }
    stages{
        stage("first stage")
        {
            steps{
                sh "echo host IP add is"
                sh "hostname -I"
                sh "echo $ENV_URL"
                sh "echo User is $CRED_USR"
                sh "mvn --version"
            }            
        }
        stage("second stage")
        {
            tools{
                maven 'mvn-395'
            }
            steps{
                sh "env"
                sh "sleep 1"
                sh "mvn --version"
            } 
        }
        stage("third stage")
        {
            steps{
                sh "echo Hii"
            } 
        }   
        stage("Testing")
        {
            parallel{   
                stage("Unit testing")
                {
                    steps{
                        sh "echo Unit testing"
                        sh "sleep 20"
                    } 
                } 
                stage("Functional testing")
                {
                    steps{
                        sh "echo Functional testing"
                        sh "sleep 20"
                    } 
                } 
                stage("Integration testing")
                {
                    steps{
                        sh "echo Integration testing"
                        sh "sleep 20"
                    } 
                }                                 
            }
        }            
    }
}