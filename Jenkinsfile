pipeline {   

   
  agent any
     tools {
        "org.jenkinsci.plugins.terraform.TerraformInstallation" "terraform-0.12.5"
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
