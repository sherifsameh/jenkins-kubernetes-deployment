  pipeline {

  environment {
    dockerimagename = "sherifsameh/react-app"
    dockerImage = ""
  }

  agent any

  stages {
 stage('Checkout Source') {
      steps {
        git 'https://github.com/sherifsameh/jenkins-kubernetes-deployment.git'
      }
    }
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

     stage('Deploy React app Image to Kubernetes') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
        sh 'kubectl apply -f service.yaml'
      }
    }
  }

}
