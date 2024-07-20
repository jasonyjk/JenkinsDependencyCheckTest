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
                dependencyCheck additionalArguments: ''' 
                    -o './'
                    -s './'
                    -f 'ALL' 
                    --prettyPrint''', odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                
                dependencyCheckPublisher pattern: 'dependency-check-report.xml'
            }
        }
    }
}
