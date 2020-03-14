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
            post {
                success {
                    slackSend color: 'good', message: 'Build Succeeded: {$GIT_BRANCH} ${JOB_NAME}-${BUILD_NUMBER}'
                }
            }
        }
        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying....'
                slackSend color: 'good', message: 'Deployed'
            }
        }
    }
}
