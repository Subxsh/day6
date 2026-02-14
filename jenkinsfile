pipeline {
    agent any

    parameters {
        string(name: 'AMI_ID', defaultValue: 'ami-073130f74f5ffb161')
    }

    stages {
        stage('Terraform Deploy') {
            steps {
                echo "Deploying with AMI_ID=${params.AMI_ID}"

                sh 'terraform init'
                sh "terraform plan -var='ami_id=${params.AMI_ID}'"
                sh "terraform apply -var='ami_id=${params.AMI_ID}' -auto-approve"
            }
        }
    }
}
