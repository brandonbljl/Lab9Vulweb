pipeline {
    agent any
    stages {
        stage ('Checkout') {
            steps {
                git branch:'master', url: 'https://github.com/OWASP/Vulnerable-Web-Application.git'
            }
        }
        stage('Code Quality Check via SonarQube') {
            steps {
                script {
                    def scannerHome = tool 'SonarQube';
                        withSonarQubeEnv('SonarQube') {
                            sh '''
                            /var/jenkins_home/tools/hudson.plugins.sonar.SonarRunnerInstallation/SonarQube/bin/sonar-scanner \
                            -Dsonar.projectKey=OWASP \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://192.168.50.187:9000 \
                            -Dsonar.token=sqp_d3c437cd7a767c02aeca3070ca7530f6ed8c1121
                            '''
                        }
                }
            }
        }
    }
    post {
        always {
            recordIssues enabledForFailure: true, tool: sonarQube()
        }
    }
}