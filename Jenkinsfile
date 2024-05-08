pipeline {
    agent any
    
    stages {
        stage('Install Apache2') {
            steps {
                sh 'sudo apt-get update'
                sh 'sudo apt-get install -y apache2'
            }
        }
        stage('Read Log File') {
            steps {
                script {
                    def logFileContent = sh(script: 'sudo cat /var/log/apache2/access.log', returnStdout: true).trim()
                    def errorLines = logFileContent.readLines().findAll { line ->
                        line =~ /(?:4\d{2}|5\d{2})/
                    }
                    if (errorLines) {
                        echo "Found errors in Apache2 access log:"
                        echo errorLines.join('\n')
                    } else {
                        echo "No errors found in Apache2 access log."
                    }
                }
            }
        }
    }
}
