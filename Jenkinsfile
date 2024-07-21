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
        stage('Dependency-Check Vulnerabilities') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'NVD-API-KEY', variable: 'NVD_API_KEY')]) {
                        dependencyCheck additionalArguments: """
                            --format HTML --format XML
                            --noupdate
                            --suppression suppression.xml
                            -o './dependency-check-report'
                            -s './'
                            --prettyPrint
                            --nvdApiKey \${NVD_API_KEY}
                        """, odcInstallation: 'OWASP Dependency-Check Vulnerabilities'
                    }
                    archiveArtifacts artifacts: 'dependency-check-report/*.xml,dependency-check-report/*.html', allowEmptyArchive: false
                    dependencyCheckPublisher pattern: '**/dependency-check-report/*.xml'
                }
            }
        }
    }
}