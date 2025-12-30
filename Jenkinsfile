pipeline {
    agent any

    environment {
        EMAIL_RECIPIENT = 'roshandeepsingh75@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the React application..'
                echo 'Tool Used: npm'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                echo 'Tool Used: Jest'
            }
            post {
                always {
                    emailext(
                        to: "${EMAIL_RECIPIENT}",
                        subject: "TEST STAGE STATUS: ${currentBuild.currentResult}",
                        body: "Unit & Integration Tests finished.\nStatus: ${currentBuild.currentResult}",
                        attachLog: true
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing static code analysis...'
                echo 'Tool Used: ESLint, SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan...'
                echo 'Tool Used: OWASP Dependency Check'
            }
            post {
                always {
                    emailext(
                        to: "${EMAIL_RECIPIENT}",
                        subject: "SECURITY SCAN STATUS: ${currentBuild.currentResult}",
                        body: "Security Scan finished.\nStatus: ${currentBuild.currentResult}",
                        attachLog: true
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging...'
                echo 'Tool Used: Docker, Nginx'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                echo 'Tool Used: Selenium'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production...'
                echo 'Tool Used: Docker, Nginx'
            }
        }
    }

    post {
        success {
            emailext(
                to: "${EMAIL_RECIPIENT}",
                subject: 'PIPELINE SUCCESS',
                body: 'Entire pipeline executed successfully.',
                attachLog: true
            )
        }
        failure {
            emailext(
                to: "${EMAIL_RECIPIENT}",
                subject: 'PIPELINE FAILED',
                body: 'Pipeline failed. Check logs.',
                attachLog: true
            )
        }
    }
}
