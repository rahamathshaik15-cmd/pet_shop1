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
            -Dsonar.projectKey=pet_shop \
            -Dsonar.projectName=pet_shop
          '''
        }
      }
    }

    stage('Quality Gate') {
      steps {
        timeout(time: 5, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}
