pipeline {

  environment {
    dockerimagename = "teknopathshala/react-app"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/TeknoPathshala/kubernetes'
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
