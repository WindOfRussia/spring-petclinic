pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh './mvnw spring-javaformat:apply'
        sh 'mvn clean test'
      }
    }
  }
}
