pipeline {
    agent any
    
    stages {
        stage('Git Pull') {
            steps {
                echo 'Pulling repository...'
                git "https://github.com/lorenz075/WebGoatPipelineTeste"
            }
        }

        stage('Check Main Branch') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'main') {
                        echo 'Running on the main branch...'
                    } else {
                        echo 'Not on the main branch, skipping subsequent stages...'
                        currentBuild.result = 'SUCCESS'
                        error('Not on the main branch')
                    }
                }
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
