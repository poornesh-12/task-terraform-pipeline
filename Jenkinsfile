pipeline {
  agent any

  environment {
    ARM_CLIENT_ID       = credentials('ARM_CLIENT_ID')
    ARM_CLIENT_SECRET   = credentials('ARM_CLIENT_SECRET')
    ARM_TENANT_ID       = credentials('ARM_TENANT_ID')
    ARM_SUBSCRIPTION_ID = credentials('ARM_SUBSCRIPTION_ID')
  }

  stages {

    stage('Checkout Terraform Code') {
      steps {
        git branch: 'main',
            url: 'https://github.com/<your-org>/terraform-azure-vm.git'
      }
    }

    stage('Terraform Init') {
      steps {
        sh 'terraform init'
      }
    }

    stage('Terraform Plan') {
      steps {
        sh 'terraform plan'
      }
    }

    stage('Terraform Apply') {
      steps {
        input message: "Apply Terraform changes?"
        sh 'terraform apply -auto-approve'
      }
    }
  }

  post {
    success {
      echo "VM successfully created in Azure!"
    }
    failure {
      echo "Terraform pipeline failed."
    }
  }
}
