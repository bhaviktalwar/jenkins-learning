pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building application'
            }
        }
    }

    post {
        success {
            emailext(
                to: 'bhaviktalwar290@gmail.com',
                subject: "JENKINS BUILD SUCCESS #${env.BUILD_NUMBER}",
                body: """Build SUCCESS

Job: ${env.JOB_NAME}
Build: ${env.BUILD_NUMBER}
URL: ${env.BUILD_URL}
""",
                attachLog: true
            )
        }
        failure {
            emailext(
                to: 'bhaviktalwar290@gmail.com',
                subject: "JENKINS BUILD FAILED #${env.BUILD_NUMBER}",
                body: """Build FAILED

Job: ${env.JOB_NAME}
Build: ${env.BUILD_NUMBER}
URL: ${env.BUILD_URL}
""",
                attachLog: true
            )
        }
    }
}
//hi
