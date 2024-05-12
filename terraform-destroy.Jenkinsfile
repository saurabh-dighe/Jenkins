pipeline {
    agent { label 'ws' } 

    options {
        //ansiColor('xterm')
        buildDiscarder(logRotator(numToKeepStr: '5')) 
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES')
    }
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select the environment')
    }
    stages {
        stage('Terraform VPC'){
            steps{
                dir('VPC') {
                git branch: 'main', url: 'https://github.com/saurabh-dighe/terraform-vpc.git'
                        sh '''
                            terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars 
                        '''
                }
            }
        }

        stage('Terraform Databases'){
            steps{
                dir('DB') {
                git branch: 'main', url: 'https://github.com/saurabh-dighe/terraform-databases.git'
                        sh '''
                            terraform destroy -auto-approve -var-file=env-${ENV}/${ENV}.tfvars 
                        '''
                }
            }
        }

    }
}