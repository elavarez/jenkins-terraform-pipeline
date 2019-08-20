pipeline {   

    agent any
    tools {
        "org.jenkinsci.plugins.terraform.TerraformInstallation" "terraform-0.12.6"
    }

    environment {
        TF_HOME = tool('terraform-0.12.6')
        TF_IN_AUTOMATION = "true"
        PATH = "$TF_HOME:$PATH"
       # DYNAMODB_STATELOCK = "ddt-tfstatelock"
       # NETWORKING_BUCKET = "ddt-networking"
      #  NETWORKING_ACCESS_KEY = credentials('networking_access_key')
     #   NETWORKING_SECRET_KEY = credentials('networking_secret_key')
    }
  stages {
    stage('checkout') {
      steps {
        checkout scm
        sh ''
      }
    }
    stage('init') {
      steps { 
         sh 'terraform --version'
        sh 'terraform  init'
      }
    }
    stage('plan') {
      steps {
        sh 'terraform plan'
      }
    }
    stage('approval') {
      options {
        timeout(time: 1, unit: 'HOURS') 
      }
      steps {
        input 'approve the plan to proceed and apply'
      }
    }
    stage('apply') {
      steps {
        sh 'terraform apply -auto-approve'
        cleanWs()
      }
    }
  }
}
