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

    stage('Pushing Image') {
      environment {
        registryCredential = 'DockerHub' // Replace with the actual credential ID
      }
      steps{
        script {
          docker.withRegistry('https://hub.docker.com', registryCredential) {
            dockerImage.push("latest")
          }
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
