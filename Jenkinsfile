pipeline {
  agent any

  tools {
    maven 'Default Maven'
  }

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build & SonarQube Analysis') {
      steps {
        withSonarQubeEnv('SonarQube') {
          sh '''
            mvn clean verify sonar:sonar \
            -Dsonar.projectKey=petshop \
            -Dsonar.projectName=petshop
          '''
        }
      }
    }

   
  }
}
