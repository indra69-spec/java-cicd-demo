pipeline {
    agent any
    tools {
        maven 'Maven-3.9.6' // Matches the name in Global Tool Configuration
    }
    triggers {
        cron('H/15 * * * *') // Triggers the pipeline every 15 minutes
    }
    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com'
            }
        }
        stage('Build & Test') {
            steps {
                sh 'mvn clean package' // Compiles and runs JUnit tests
            }
        }
        stage('Docker Build & Push') {
            steps {
                script {
                    docker.withRegistry('', 'docker-hub-creds') {
                        def appImage = docker.build("your-dockerhub-id/java-app:${env.BUILD_NUMBER}")
                        appImage.push()
                    }
                }
            }
        }
    }
}
