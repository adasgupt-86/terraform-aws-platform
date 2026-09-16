pipeline {
    agent any

    environment {
        TF_IN_AUTOMATION = 'true'
        AWS_DEFAULT_REGION = 'ap-south-1'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Terraform Format') {
            steps {
                dir('environments/dev') {
                    sh 'terraform fmt -check -recursive'
                }
            }
        }

        stage('Terraform Init') {
            steps {
                dir('environments/dev') {
                    sh 'terraform init -input=false'
                }
            }
        }

        stage('Terraform Validate') {
            steps {
                dir('environments/dev') {
                    sh 'terraform validate'
                }
            }
        }

        stage('Terraform Plan') {
            steps {
                withCredentials([
                    [$class: 'AmazonWebServicesCredentialsBinding',
                     credentialsId: 'aws-terraform-lab']
                ]) {
                    dir('environments/dev') {
                        sh '''
                            terraform plan \
                              -input=false \
                              -var="bucket_name=abhisheks-application-bucket" \
                              -var="environment=dev" \
                              -out=tfplan
                        '''
                    }
                }
            }
        }
    }

    post {
        always {
            echo 'Terraform CI pipeline finished.'
        }
    }
}