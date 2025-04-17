pipeline {
    agent any

    environment {
        SONARQUBE_SERVER = 'SonarQube'  // The name of the SonarQube server configured in Jenkins
        SONAR_TOKEN = 'squ_c6b3c430a79f09f15a7bbed4d574b797c7f0ecbd' // Store the token securely
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ArmasNevolainen/week5'
            }
        }

        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQubeServer') {
                    bat """
                        sonar-scanner ^
                        -Dsonar.projectKey=devops-demo ^
                        -Dsonar.sources=src ^
                        -Dsonar.projectName=DevOps-Demo ^
                        -Dsonar.host.url=http://localhost:9000 ^
                        -Dsonar.login=${env.SONAR_TOKEN} ^
                        -Dsonar.java.binaries=target/classes
                    """
                }
            }
        }

    }
}
