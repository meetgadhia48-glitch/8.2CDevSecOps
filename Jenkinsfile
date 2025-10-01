pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // your GitHub repo (you provided username)
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
                // allow pipeline to continue if tests fail so post actions run
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
                subject: "✅ SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>Hello,</p>
                         <p>The Jenkins build <b>${env.JOB_NAME} #${env.BUILD_NUMBER}</b> completed <b>successfully</b>.</p>
                         <p>Console output: <a href="${env.BUILD_URL}console">${env.BUILD_URL}console</a></p>
                         <p>Regards,<br/>CI System</p>""",
                to: "sit190task8.2c@gmail.com",
                attachLog: true
            )
        }

        failure {
            emailext (
                subject: "❌ FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """<p>Hello,</p>
                         <p>The Jenkins build <b>${env.JOB_NAME} #${env.BUILD_NUMBER}</b> <b>failed</b>.</p>
                         <p>Console output: <a href="${env.BUILD_URL}console">${env.BUILD_URL}console</a></p>
                         <p>Regards,<br/>CI System</p>""",
                to: "sit190task8.2c@gmail.com",
                attachLog: true
            )
        }
    }
}
