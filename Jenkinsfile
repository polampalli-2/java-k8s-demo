pipeline {
  agent any

  environment {
    IMAGE_NAME = "surendrakumar2/demo-app"
  }

  stages {
    stage('Checkout') {
      steps {
        https://github.com/polampalli-2/java-k8s-demo.git
      }
    }

    stage('Build Jar') {
      steps {
        sh 'mvn clean package -DskipTests'
      }
    }

    stage('Docker Build & Push') {
      steps {
        script {
          def app = docker.build("${IMAGE_NAME}:latest")
          docker.withRegistry('https://index.docker.io/v1/', 'dockerhub-credentials') {
            app.push()
          }
        }
      }
    }

    stage('K8s Deploy') {
      steps {
        sh 'kubectl apply -f deployment.yaml'
        sh 'kubectl apply -f service.yaml'
      }
    }
  }
}
