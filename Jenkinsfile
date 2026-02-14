pipeline {
    agent any

    parameters {
        string(name: 'AMI_ID', defaultValue: 'ami-073130f74f5ffb161')
        string(name: 'AWS_CREDENTIALS_ID', defaultValue: 'aws-jenkins-creds')
    }

    environment {
        AMI_ID = "${params.AMI_ID}"
    }

    stages {
        stage('Terraform Deploy') {
            steps {
                echo "Deploying with AMI_ID=${AMI_ID}"

                sh '''
                    if [ -z "$AMI_ID" ]; then
                        echo "AMI_ID is required"
                        exit 1
                    fi
                '''

                withCredentials([
                    [$class: 'AmazonWebServicesCredentialsBinding',
                     credentialsId: params.AWS_CREDENTIALS_ID]
                ]) {
                    sh 'terraform init'
                    sh "terraform plan -var='ami_id=${AMI_ID}'"
                    sh "terraform apply -var='ami_id=${AMI_ID}' -auto-approve"
                }
            }
        }
    }
}
