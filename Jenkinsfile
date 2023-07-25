  pipeline {

  environment {
    dockerimagename = "bravinwasike/react-app"
    dockerImage = ""
  }

  agent any

  stages {

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'Docker'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ) {
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
