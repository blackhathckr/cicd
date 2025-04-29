pipeline {
    agent any

    environment {
        // Define JDK path if needed, or ensure JAVA_HOME is globally set
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clone Repo') {
            steps {
                git 'https://github.com/blackhathckr/cicd.git'
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x gradlew'
                sh './gradlew clean build'
            }
        }

        stage('Test') {
            steps {
                sh './gradlew test'
            }
        }

        stage('Deploy') {
            steps {
                // This is optional depending on your project
                // You can replace this with a `scp`, `docker build`, or `java -jar build/libs/*.jar`
                sh 'java -jar build/libs/*.jar &'
            }
        }
    }

    post {
        success {
            echo '✅ Build and Deployment Successful!'
        }
        failure {
            echo '❌ Build or Deployment Failed.'
        }
    }
}
