pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo 'Source code checked out from GitHub'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat 'mvn sonar:sonar -Dsonar.projectKey=DevOpsPipeline -Dsonar.projectName=DevOpsPipeline'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Testing completed'
            }
        }
    }

    post {
        success {
            echo 'DevOps Pipeline completed successfully!'
        }

        failure {
            echo 'DevOps Pipeline failed. Check the console output.'
        }
    }
}