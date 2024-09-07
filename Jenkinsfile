pipeline {
    agent any
    environment {
        EMAIL_RECIPIENTS = 'sadesrashmika12@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven...'
                echo 'Tool: Maven'
                // Simulate build process
                bat 'echo Building project...'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit and integration tests...'
                echo 'Tools: JUnit for unit tests, TestNG for integration tests'
                // Create dummy log files for demonstration
                bat 'echo Creating unit-test.log > unit-test.log'
                bat 'echo Creating integration-test.log > integration-test.log'
            }
            post {
                success {
                    archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
                    emailext (
                        subject: "Unit and Integration Tests SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Unit and integration tests passed successfully. Logs are attached.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachLog: true,
                        attachmentsPattern: "*.log"
                    )
                }
                failure {
                    archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
                    emailext (
                        subject: "Unit and Integration Tests FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Unit and integration tests failed. Logs are attached.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachLog: true,
                        attachmentsPattern: "*.log"
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis with SonarQube...'
                echo 'Tool: SonarQube'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan using OWASP Dependency-Check...'
                echo 'Tool: OWASP Dependency-Check'
                // Create a dummy security scan log
                bat 'echo Creating security-scan.log > security-scan.log'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'security-scan.log', allowEmptyArchive: true
                    emailext (
                        subject: "Security Scan SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Security scan passed successfully. Logs are attached.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachLog: true,
                        attachmentsPattern: "security-scan.log"
                    )
                }
                failure {
                    archiveArtifacts artifacts: 'security-scan.log', allowEmptyArchive: true
                    emailext (
                        subject: "Security Scan FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Security scan failed. Logs are attached.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachLog: true,
                        attachmentsPattern: "security-scan.log"
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to staging...'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to production...'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
        }

        success {
            emailext (
                subject: "SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                body: "Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] succeeded. Logs are attached.",
                to: "${env.EMAIL_RECIPIENTS}",
                attachLog: true,
                attachmentsPattern: "*.log"
            )
        }

        failure {
            emailext (
                subject: "FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                body: "Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] failed. Logs are attached.",
                to: "${env.EMAIL_RECIPIENTS}",
                attachLog: true,
                attachmentsPattern: "*.log"
            )
        }
    }
}
