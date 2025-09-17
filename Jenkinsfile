pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/meetgadhia48-glitch/8.2CDevSecOps.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm ci'
            }
        }
        stage('Run Tests') {
            steps {
                sh 'npm test || true'
            }
        }
        stage('Generate Coverage Report') {
            steps {
                sh 'npm run coverage || true'
            }
        }
        stage('NPM Audit (Security Scan)') {
            steps {
                sh 'npm audit || true'
            }
        }
    }
    post {
        success {
            emailext (
                subject: "SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>Build succeeded!</p>
                         <p>Check the console: <a href="${env.BUILD_URL}console">${env.BUILD_URL}console</a></p>""",
                to: "YOUR_MAILTRAP_TEST_EMAIL@inbox.mailtrap.io",
                attachLog: true
            )
        }
        failure {
            emailext (
                subject: "FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>Build failed!</p>
                         <p>Check the console: <a href="${env.BUILD_URL}console">${env.BUILD_URL}console</a></p>""",
                to: "YOUR_MAILTRAP_TEST_EMAIL@inbox.mailtrap.io",
                attachLog: true
            )
        }
    }
}
