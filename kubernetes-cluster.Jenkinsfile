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
                    sudo make create
                '''
            }
        }
        stage('Cluster Infra Deletion') {
            when {
                expression { params.ACTION == 'destroy'}
            }
            steps {        
                sh '''
                    cd /home/centos/kubernetes/eks
                    sudo make destroy
                '''
            } 
        }
    }
}