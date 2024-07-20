pipeline {
    agent any
    stages {
        stage('Checkout SCM') {
            steps {
                script {
                    git branch: "master",
                        url: "https://github.com/jasonyjk/JenkinsDependencyCheckTest.git"
                }
            }
        }
		stage('OWASP Dependency-Check Vulnerabilities') {
            steps {
                dependencyCheck additionalArguments: '--format HTML --format XML --noupdate --suppression suppression.xml', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
            }
        }
    }   
    post {
        success {
            dependencyCheckPublisher pattern: 'dependency-check-report.xml'
        }
    }
}
