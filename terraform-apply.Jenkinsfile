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
    }
    stages {
        stage('Terraform VPC'){
            steps{
                dir('VPC') {
                        sh "rm -rf ./VPC/*"
                git branch: 'main', url: 'https://github.com/saurabh-dighe/terraform-vpc.git'
                        sh '''
                            terrafile -f ./env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                            terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars 
                        '''
                }
            }
        }
        stage('Terraform ALB'){
            steps{
                dir('DB') {
                git branch: 'main', url: 'https://github.com/saurabh-dighe/terraform-loadbalancers.git'
                        sh '''
                            terrafile -f ./env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                            terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars 
                        '''
                }
            }
        }

        stage('Terraform Databases'){
            steps{
                dir('DB') {
                git branch: 'main', url: 'https://github.com/saurabh-dighe/terraform-databases.git'
                        sh '''
                            terrafile -f ./env-dev/Terrafile
                            terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                            terraform plan -var-file=env-${ENV}/${ENV}.tfvars -var ENV=${ENV}
                            terraform apply -auto-approve -var-file=env-${ENV}/${ENV}.tfvars 
                        '''
                }
            }
        }
        stage('Backend'){
            parallel{
                stage('Catalogue'){
                    steps {
                        dir('catalogue') {   
                            git branch: 'main', url: 'https://github.com/saurabh-dighe/catalogue.git'

                            sh ''' 
                                cd mutable-infra
                                terrafile -f ./env-${ENV}/Terrafile
                                terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                                terraform plan -var APP_VERSION=002 --var-file env-${ENV}/${ENV}.tfvars
                                terraform apply -auto-approve -var APP_VERSION=002 --var-file env-${ENV}/${ENV}.tfvars
                            ''' 
                        }
                    }
                }
                stage('User'){
                    steps {
                        dir('user') {   
                            git branch: 'main', url: 'https://github.com/saurabh-dighe/user.git'

                            sh ''' 
                                cd mutable-infra
                                terrafile -f ./env-${ENV}/Terrafile
                                terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                                terraform plan -var APP_VERSION=001 --var-file env-${ENV}/${ENV}.tfvars
                                terraform apply -auto-approve -var APP_VERSION=001 --var-file env-${ENV}/${ENV}.tfvars
                            ''' 
                        }
                    }
                }
                stage('Cart'){
                    steps {
                        dir('cart') {   
                            git branch: 'main', url: 'https://github.com/saurabh-dighe/cart.git'

                            sh ''' 
                                cd mutable-infra
                                terrafile -f ./env-${ENV}/Terrafile
                                terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                                terraform plan -var APP_VERSION=001 --var-file env-${ENV}/${ENV}.tfvars
                                terraform apply -auto-approve -var APP_VERSION=001 --var-file env-${ENV}/${ENV}.tfvars
                            ''' 
                        }
                    }
                }
                stage('Shipping'){
                    steps {
                        dir('shipping') {   
                            git branch: 'main', url: 'https://github.com/saurabh-dighe/shipping.git'

                            sh ''' 
                                cd mutable-infra
                                terrafile -f ./env-${ENV}/Terrafile
                                terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                                terraform plan -var APP_VERSION=001 --var-file env-${ENV}/${ENV}.tfvars
                                terraform apply -auto-approve -var APP_VERSION=001 --var-file env-${ENV}/${ENV}.tfvars
                            ''' 
                        }
                    }
                }
                stage('Payment'){
                    steps {
                        dir('payment') {   
                            git branch: 'main', url: 'https://github.com/saurabh-dighe/payment.git'

                            sh ''' 
                                cd mutable-infra
                                terrafile -f ./env-${ENV}/Terrafile
                                terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                                terraform plan -var APP_VERSION=001 --var-file env-${ENV}/${ENV}.tfvars
                                terraform apply -auto-approve -var APP_VERSION=001 --var-file env-${ENV}/${ENV}.tfvars
                            ''' 
                        }
                    }
                }
                
            }
        }
        stage('Frontend'){
            steps {
                dir('frontend') {   
                    git branch: 'main', url: 'https://github.com/saurabh-dighe/frontend.git'

                    sh ''' 
                        cd mutable-infra
                        terrafile -f ./env-${ENV}/Terrafile
                        terraform init --backend-config=env-${ENV}/backend-${ENV}.tfvars -reconfigure
                        terraform plan -var APP_VERSION=001 --var-file env-${ENV}/${ENV}.tfvars
                        terraform apply -auto-approve -var APP_VERSION=001 --var-file env-${ENV}/${ENV}.tfvars
                    ''' 
                }
            }
        }
    }
}