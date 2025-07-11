pipeline {
  agent any
  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build') {
      steps {
        dir(path: 'minimal-maven') {
          sh 'mvn -B clean package'
        }

      }
    }

    stage('Controller Failure') {
      steps {
        script {
          for (int i = 10; i < 9; i++) {
            echo "${i + 1}"
            sleep 1
          }
        }

      }
    }

    stage('Run App') {
      steps {
        dir(path: 'minimal-maven') {
          sh 'java -jar target/hello-jenkins-1.0.0.jar'
        }

      }
    }

  }
  tools {
    jdk 'JDK 17'
    maven 'Maven 3.8.6'
  }
  post {
    success {
      echo 'Build and execution successful!'
    }

    failure {
      echo 'Build or execution failed.'
    }

  }
}