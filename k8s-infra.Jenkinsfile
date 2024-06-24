pipeline {
    agent { label 'ws' } 

    options {
        ansiColor('xterm')
        buildDiscarder(logRotator(numToKeepStr: '5')) 
        disableConcurrentBuilds()
        timeout(time: 50, unit: 'MINUTES')
    }
    parameters {
        choice(name: 'ENV', choices: ['dev', 'prod'], description: 'Select the environment')
        choice(name: 'ACTION', choices: ['create', 'destroy'], description: 'Action to perform')
    }
    stages {
        stage('Terraform VPC'){
            steps{
                dir('VPC') {
                    sh "rm -rf ./VPC/*"
                git branch: 'main', url: 'https://github.com/saurabh-dighe/terraform-vpc.git'
                    sh '''
                        rm -rf
                        terrafile -f ./env-dev/Terrafile
                        terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                        terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                        terraform ${ACTION} -auto-approve -var-file=env-${ENV}/${ENV}.tfvars 
                    '''
                }
            }
        }

        stage('Kubernetes Infra'){
            steps{
                dir('k8s') {
                git branch: 'main', url: 'https://github.com/saurabh-dighe/kubernetes.git'
                    sh '''
                        cd eks
                        terrafile -f env-dev/Terrafile
                        terraform init --backend-config=env-${ENV}/${ENV}-backend.tfvars -reconfigure
                        terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                        terraform ${ACTION} -auto-approve -var-file=env-${ENV}/${ENV}.tfvars 
                    '''
                }
            }
        }
        stage('Terraform Databases'){
            steps{
                dir('DB') {
                    sh "rm -rf ./DB/*"
                git branch: 'main', url: 'https://github.com/saurabh-dighe/terraform-databases.git'
                    sh '''
                        rm -rf
                        terrafile -f ./env-dev/Terrafile
                        terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                        terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                        terraform ${ACTION} -auto-approve -var-file=env-${ENV}/${ENV}.tfvars 
                    '''
                }
            }
        }
    }
}