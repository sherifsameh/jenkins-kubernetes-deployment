  pipeline {

  environment {
    dockerimagename = "sherif/react-app:latest"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build ("sherif/react-app:latest")
        }
      }
    }

    stage('Tag Image') {
      steps{
        script {
             dockerImage.tag("sherif/react-app:ReactApp")
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
