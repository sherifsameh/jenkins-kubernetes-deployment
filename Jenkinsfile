  pipeline {

  environment {
    dockerimagename = "react-app:latest"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build ("react-app:latest")
        }
      }
    }
     stage('Tag image') {
      steps{
        script {
          dockerImage = docker.tag ("sherifsameh/react-app:ReactAppv1")
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'Docker'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential )
          {
             dockerImage.push()
          }
        }
      }
    }

    stage('Deploying React.js container to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml")
        }
      }
    }

  }

}
