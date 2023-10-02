pipeline {

  environment {
    dockerimagename = "bussar/react-app"
    dockerImage = ""
  }

  agent any

  stages {

   // stage('Checkout Source') {
      //steps {
        //git 'https://github.com/RAM50558/jenkins-kubernetes-deployment.git'
      //}
    //}

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build dockerimagename
        }
      }
    }

    stage('Pushing Image') {
      environment {
               registryCredential = 'dockerhub-credentials'
           }
      steps{
        script {
          docker.withRegistry( 'https://registry.hub.docker.com', dockerhub-credentials ) {
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
