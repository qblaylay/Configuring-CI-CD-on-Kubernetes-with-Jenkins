pipeline {
  agent any
  stages {
    stage('Docker Build') {
      steps {
        sh "docker build -t kozcan/podinfo:${env.BUILD_NUMBER} ."
        echo 'Build is completed. '
      
      }
    }
    stage('Docker Push') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
          sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
          echo 'Login completed. '
          sh "docker push kozcan/podinfo:${env.BUILD_NUMBER}"
          echo 'PUSH completed. '
        }
      }
    }
    /*
    stage('Docker Remove Image') {
      steps {
        sh "docker rmi kozcan/podinfo:${env.BUILD_NUMBER}"
      }
    }
   stage('Apply Kubernetes Files') {
      steps {
          withKubeConfig([credentialsId: 'kubeconfig']) {
          sh 'cat deployment.yaml | sed "s/{{BUILD_NUMBER}}/$BUILD_NUMBER/g" | kubectl apply -f -'
          sh 'kubectl apply -f service.yaml'
        }
      }
  }*/
}
  /*
post {
    success {
      slackSend(message: "Pipeline is successfully completed.")
    }
    failure {
      slackSend(message: "Pipeline failed. Please check the logs.")
    }
}
*/
}
