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
    properties([
        parameters([
            choice(name: 'ACTION', choices: ['create', 'destroy'], description: 'Action to perform')
        ])
    stages {
        stage('Cluster Infra') {
            steps {
                if (params.ACTION == 'create') {        
                    sh '''
                        sh rm -rf
                        cd /home/centos/kubernetes/eks'
                        terrafile -f  env-dev/Terrafile
                        terraform init -backend-config=env-dev/dev-backend.tfvars -reconfigure
                        terraform apply -auto-approve -var-file=env-dev/dev.tfvars
                    '''
                }
                else if (params.ACTION == 'destroy') {        
                    sh '''
                        sh rm -rf
                        cd /home/centos/kubernetes/eks'
                        terrafile -f  env-dev/Terrafile
                        terraform init -backend-config=env-dev/dev-backend.tfvars -reconfigure
                        terraform destroy -auto-approve -var-file=env-dev/dev.tfvars
                    '''
                }
            }
        }
    }
}