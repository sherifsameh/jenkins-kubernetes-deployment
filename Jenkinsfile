  pipeline {

  environment {
    dockerimagename = "reactapp"
    dockerImage = ""
  }

  agent any

  stages {

   stage('Build Docker image') {
            steps {
                echo "-=- build Docker image -=-"
                sh "docker build -t sherifsameh/reactapp:v1 ."
            }
        }
     stage('Tag image') {
      steps{
        sh "docker tag reactapp:latest  sherifsameh/reactapp:v1"
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
