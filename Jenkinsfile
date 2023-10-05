pipeline {
  environment {
    dockerimagename = "teknopathshala/react-app"
  }

  agent any

  stages {
    stage('Checkout Source') {
      steps {
        git branch: 'main', url: 'https://github.com/TeknoPathshala/kubernetes'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    
    stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }
  }
}
