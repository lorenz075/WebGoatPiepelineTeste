pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    
    stages {
        stage('Git Pull') {
            steps {
                echo 'Pulling repository...'
                git url: "https://github.com/lorenz075/WebGoatPipelineTeste", branch: 'main'
            }
        }

        
        stage('OWASP Dependency Checker') {
            steps {
                echo 'Testing..'
                dependencyCheck additionalArguments: '', odcInstallation: 'Default'
            }
        }

        stage('OWASP Report') {
            steps {
                echo 'Generating report..'
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }

        stage('SonarQube Analysis') {
            steps{
                withSonarQubeEnv('SonarQubeLocal') {
                  sh 'mvn sonar:sonar -Dsonar.projectKey=WebGoatPipelineTeste -Dsonar.host.url=http://127.0.0.1:9000'

            }
        }
      }
        
        stage('Build') {
            steps {
                echo 'Done'
            }
        }
    }
}
