pipeline {
    agent any

    parameters {
        string(
            name: 'AMI_ID',
            defaultValue: 'ami-073130f74f5ffb161',
            description: 'Amazon Machine Image (AMI) ID to use for the EC2 instance'
        )
        string(
            name: 'AWS_CREDENTIALS_ID',
            defaultValue: 'aws-jenkins-creds',
            description: 'Jenkins AWS credentials ID'
        )
    }

    stages {
        stage('Terraform Deploy') {
            steps {
                echo 'Deploying...'

                // Validate AMI_ID
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
                    sh "terraform plan -var=\"ami_id=${AMI_ID}\""
                    sh "terraform apply -var=\"ami_id=${AMI_ID}\" -auto-approve"
                }
            }
        }
    }
}
