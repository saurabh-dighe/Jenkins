pipeline {
    agent{
        label 'ws'
    }
    options {
        ansiColor('xterm')
        buildDiscarder(logRotator(numToKeepStr: '5')) 
        disableConcurrentBuilds()
        timeout(time: 50, unit: 'MINUTES')
    }
    parameters{
        choice(name: 'ACTION', choices: ['create', 'destroy'], description: 'Action to perform')
    }
    stages {
        stage('Cluster Infra Creation') {
            when {
                expression { params.ACTION == 'create'}
            }
            steps {
                sh '''
                    cd /home/centos/kubernetes/eks
                    terrafile -f  env-dev/Terrafile
                    terraform init -backend-config=env-dev/dev-backend.tfvars -reconfigure
                    terraform apply -auto-approve -var-file=env-dev/dev.tfvars
                '''
            }
        }
        stage('Cluster Infra Deletion') {
            when {
                expression { params.ACTION == 'destroy'}
            }
            steps {        
                sh '''
                    rm -rf
                    cd /home/centos/kubernetes/eks
                    terrafile -f  env-dev/Terrafile
                    terraform init -backend-config=env-dev/dev-backend.tfvars -reconfigure
                    terraform destroy -auto-approve -var-file=env-dev/dev.tfvars
                '''
            } 
        }
    }
}