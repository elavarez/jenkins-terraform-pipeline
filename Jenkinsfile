pipeline {   
      agent any
   
  agent {
    node {
      label 'master'
    }  
  }
     tools {
        "org.jenkinsci.plugins.terraform.TerraformInstallation" "terraform-0.12.6"
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
