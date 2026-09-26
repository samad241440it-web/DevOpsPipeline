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

        stage('Docker Build') {
            steps {
                bat '"C:\\Users\\admin\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" build -t devopspipeline:1.0 .'
            }
        }

        stage('Docker Run') {
            steps {
                bat '''
                    "C:\\Users\\admin\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" rm -f devopspipeline-container 2>NUL
                    "C:\\Users\\admin\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin\\docker.exe" run --name devopspipeline-container devopspipeline:1.0
                '''
            }
        }
    }

    post {
        success {
            echo 'End-to-End DevOps Pipeline completed successfully!'
        }

        failure {
            echo 'DevOps Pipeline failed. Check the console output.'
        }
    }
}