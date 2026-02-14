pipeline{
    agent any
    stages {
        stage('source code') {
            steps {
                echo 'Cloning...'
                   git branch: 'main', url: 'https://github.com/PV-Sudarsan/task-jenkins.git'

            }
        }
        stage('terraform') {
            steps {
                echo 'Deploying...'
                sh 'terraform init'
                sh 'terraform plan -var="ami=ami-0abc1234def567890" '
                sh 'terraform apply -var="ami=ami-0abc1234def567890" -auto-approve'
            }
        }
    }
}