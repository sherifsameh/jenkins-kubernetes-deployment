  pipeline {

  environment {
    dockerimagename = "sherifsameh/react-app"
    dockerImage = ""
  }

  agent any

  stages {
   stage('Build image') {
      steps{
        script {
          dockerImage = docker.build ("sherifsameh/react-app")
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
		  dockerImage.push("latest")
          }
        }
      }
       }
	  stage('Deploying App to Kubernetes') {
      steps {
        script {
          kubernetesDeploy(configs: "deployment.yaml", "service.yaml", kubeconfigId: "kubernetes")
        }
      }
    }
	
  }

}
