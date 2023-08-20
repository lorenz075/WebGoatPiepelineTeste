pipeline {
    agent any
    tools {
        maven 'Default Maven'
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
                  bat "${tool("SonarQubeScanner")}/bin/sonar-scanner  \
                    -Dsonar.projectKey=WebGoatPipelineTeste \
                    -Dsonar.projectName='WebGoatPipelineTeste' "   
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
