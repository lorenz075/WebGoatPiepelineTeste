pipeline {
    agent any
    
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
        stage('Build') {
            steps {
                echo 'Done'
            }
        }
    }
}
