pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './mvnw clean compile'
      }
    }

    stage('Unit Test') {
      steps {
        sh './mvnw test'
        junit '**/target/surefire-reports/TEST-*.xml'
      }
    }

    stage('Static Analysis') {
      steps {
        sh '''./mvnw sonar:sonar \\
  -Dsonar.projectKey=JPetstore \\
  -Dsonar.projectName=\'JPetstore\' \\
  -Dsonar.host.url=http://13.201.170.249:9000 \\
  -Dsonar.token=sqp_7fb32382c438c6fc3abd00416cadaf5c4d5df1dc'''
      }
    }

    stage('Package') {
      steps {
        sh './mvnw package -DskipTests=true'
      }
    }

  }
}