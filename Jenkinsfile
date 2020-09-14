pipeline {
  agent any
  parameters {
    password (name: 'DIGITALOCEAN_TOKEN')
  }
  environment {
    TF_WORKSPACE = 'dev' //Sets the Terraform Workspace
    TF_IN_AUTOMATION = 'true'
    DIGITALOCEAN_TOKEN = credentials('DIGITALOCEAN_TOKEN')
    TERRAFORM_HOME = "/usr/bin"
  }
  stages {
    stage('Terraform Init') {
      steps {
        sh "${env.TERRAFORM_HOME}/terraform init -input=false"
      }
    }
    stage('Terraform Plan') {
      steps {
        echo "${env.DIGITALOCEAN_TOKEN}"
        sh "${env.TERRAFORM_HOME}/terraform plan -out=tfplan -input=false -var-file='dev.tfvars'"
      }
    }
    stage('Terraform Apply') {
      steps {
        sh "${env.TERRAFORM_HOME}/terraform apply -auto-approve -input=false tfplan"
      }
    }
    stage('Terraform Destroy') {
      steps {
        sh "${env.TERRAFORM_HOME}/terraform destroy -auto-approve"
      }
    }
   }
}
