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
		 dockerImage.push("${BUILD_NUMBER}")
          }
        }
      }
    }

     stage('Deploy Reach Image to Kubernetes') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
        sh 'kubectl apply -f service.yaml'
      }
    }
  }

}
