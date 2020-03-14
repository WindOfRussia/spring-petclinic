pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn -B -DskipTests clean install'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
      post {
        always {
          junit 'target/surefire-reports/**/*.xml'
        }
      }
    }
    stage('Package') {
      steps {
        sh './mvnw package'
      }
    }
    if (env.BRANCH_NAME == "mater" ) {
      stage('Deploy') {
        steps {
          echo 'Deployed'
          echo 'notify slack'
        }
      }
    }
  }
}
