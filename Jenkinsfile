pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'bhaviktalwar290@gmail.com'
    }

    stages {

        stage('Build') {
            steps {
                echo 'Building the application'
                echo 'Tool: Maven / npm'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests'
                echo 'Tool: JUnit / Jest'
            }
            post {
                always {
                    emailext(
                        to: "${EMAIL_RECIPIENT}",
                        subject: "TEST STAGE: ${currentBuild.currentResult}",
                        body: """Unit & Integration Tests completed.
Status: ${currentBuild.currentResult}
Job: ${env.JOB_NAME}
Build: #${env.BUILD_NUMBER}
""",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Running code analysis'
                echo 'Tool: SonarQube / ESLint'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan'
                echo 'Tool: OWASP Dependency Check'
            }
            post {
                always {
                    emailext(
                        to: "${EMAIL_RECIPIENT}",
                        subject: "SECURITY SCAN: ${currentBuild.currentResult}",
                        body: """Security Scan completed.
Status: ${currentBuild.currentResult}
Job: ${env.JOB_NAME}
Build: #${env.BUILD_NUMBER}
""",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging'
                echo 'Tool: Docker / AWS EC2'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging'
                echo 'Tool: Selenium'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production'
                echo 'Tool: Docker / AWS EC2'
            }
        }
    }
}
