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
                    slackSend color: 'good', message: "Build Succeeded: {$env.GIT_BRANCH} | ${env.JOB_NAME}-${env.BUILD_NUMBER} | ${env.BUILD_STATUS}"
                }
                failure {
                    slackSend color: 'bad', message: "Build Failed: {$env.GIT_BRANCH} | ${env.JOB_NAME}-${env.BUILD_NUMBER} | ${env.BUILD_STATUS}"
                }
            }
        }
        stage('Deploy') {
            when {
                branch 'master'
            }
            steps {
                echo 'Deploying....'
                slackSend color: 'good', message: "{$env.GIT_BRANCH} Deployed"
            }
        }
    }
}
