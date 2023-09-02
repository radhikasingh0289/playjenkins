pipeline {

  environment {
    registry = "radhikasinghkirar/playjenkins"
    dockerImage = ""
    KUBECONFIG = credentials('kubeconfigmaster')
  }

  agent any

  stages {

    stage('Checkout Source') {
      steps {
        git 'https://github.com/radhikasingh0289/playjenkins.git'
      }
    }

    stage('Build image') {
      steps{
        script {
          dockerImage = docker.build registry + ":$BUILD_NUMBER"
        }
      }
    }

    stage('Push Image') {
      steps{
        script {
          docker.withRegistry( "" ) {
            dockerImage.push()
          }
        }
      }
    }

    stage('Deploy App') {
      steps {
        script {
          sh "kubectl --kubeconfig=$KUBECONFIG apply -f myweb.yaml"
        }
      }
    }

  }

}
