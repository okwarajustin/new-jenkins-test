pipeline {
    agent any
    environment {
        AWS_REGION = 'us-east-1'
    }
    stages {
        stage('Checkout Code') {
            steps {
               // replace git URL below with your git repo url
                git branch: 'main', url: 'https://github.com/okwarajustin/new-jenkins-test.git'
            }
        }
        stage('Initialize Terraform') {
            steps {
                sh 'terraform init'
            }
        }
        stage('Plan Terraform') {
            steps {
                sh 'terraform plan -out=tfplan'
            }
        }
        stage('Apply Terraform') {
            steps {
                input message: "Approve deployment?", ok: "Deploy"
                sh 'terraform apply -auto-approve tfplan'
            }
        }
        stage('Destroy Terraform') {
            steps {
                input message: "Approve destroy?", ok: "Destroy"
                sh 'terraform destroy -auto-approve'
            }
        }
    }
}