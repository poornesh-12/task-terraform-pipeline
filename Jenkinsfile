pipeline {
    agent any

    environment {
    ARM_CLIENT_ID       = credentials('97b1adeb-9a61-4fc5-9598-4693b38a2494')
    ARM_CLIENT_SECRET   = credentials('Zzj8Q~Lh4OBqgUJ4ooAAfZZbjzxZcJGlgbAX6b0.')
    ARM_TENANT_ID       = credentials('84b72206-a90a-4751-82fe-dccd6d183246')
    ARM_SUBSCRIPTION_ID = credentials('e0d10ccd-48d7-4654-a8b4-0d881dcdeb9e')
    TF_IN_AUTOMATION = "true"
    }

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/poornesh-12/task-terraform-pipeline.git'
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
                sh 'terraform apply -auto-approve'
            }
        }
    }

    post {
        success {
            echo "Azure VM successfully created!"
        }
        failure {
            echo "Terraform execution failed"
        }
    }
}
