  pipeline {

  environment {
    dockerimagename = "sherif/react-app"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Tag Image') {
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential )
            {
             dockerImage.tag("reactappv1")
          }
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
             dockerImage.push("reactappv1")
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
