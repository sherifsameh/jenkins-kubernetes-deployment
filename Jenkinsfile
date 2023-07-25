  pipeline {

  environment {
    dockerimagename = "reactapp"
    dockerImage = ""
  }

  agent any

  stages {

   stage('Build image') {
      steps{
        script {
          dockerImage = docker.build ("reactapp")
        }
      }
    }
    stage('Pushing Image') {
      environment {
               registryCredential = 'Docker'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', registryCredential ){        
	  dockerImage.push("${BUILD_NUMBER}")
	   dockerImage.push("latest")
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
