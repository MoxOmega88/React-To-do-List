pipeline {
    agent any
    
    // This tells Jenkins to pull the tool we just configured
    tools {
        'dependency-check' 'DP-Check' 
    }

    stages {
        stage('Checkout Code') {
            steps {
                // This step pulls your code from GitHub
                checkout scm
            }
        }

        stage('OWASP Dependency-Check Scan') {
            steps {
                // This command runs the scanner on your project files
                dependencyCheck additionalArguments: '--scan ./ --format ALL', odcInstallation: 'DP-Check'
            }
        }

        stage('Publish Results and Quality Gate') {
            steps {
                // This generates the graphs and fails the build if 1 High or Critical vulnerability is found
                dependencyCheckPublisher pattern: 'dependency-check-report.xml', 
                                         failedTotalHigh: 1, 
                                         failedTotalCritical: 1
            }
        }
    }
}