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
                // Replace with the correct Maven command for Windows if Maven is installed
                bat 'echo Building project...'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit and integration tests...'
                echo 'Tools: JUnit for unit tests, TestNG for integration tests'
                // Creating dummy log files for Windows environment
                bat 'echo Creating unit-test.log > unit-test.log'
                bat 'echo Creating integration-test.log > integration-test.log'
            }
            post {
                success {
                    archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
                    mail (
                        subject: "Unit and Integration Tests SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Unit and integration tests passed successfully. Logs can be downloaded from: ${env.BUILD_URL}artifact/*.log",
                        to: "${env.EMAIL_RECIPIENTS}"
                    )
                }
                failure {
                    archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
                    mail (
                        subject: "Unit and Integration Tests FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Unit and integration tests failed. Logs can be downloaded from: ${env.BUILD_URL}artifact/*.log",
                        to: "${env.EMAIL_RECIPIENTS}"
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis with SonarQube...'
                echo 'Tool: SonarQube'
                // Add a command for code analysis if required
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan using OWASP Dependency-Check...'
                echo 'Tool: OWASP Dependency-Check'
                // Create a dummy security scan log for Windows environment
                bat 'echo Creating security-scan.log > security-scan.log'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'security-scan.log', allowEmptyArchive: true
                    mail (
                        subject: "Security Scan SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Security scan passed successfully. Logs can be downloaded from: ${env.BUILD_URL}artifact/security-scan.log",
                        to: "${env.EMAIL_RECIPIENTS}"
                    )
                }
                failure {
                    archiveArtifacts artifacts: 'security-scan.log', allowEmptyArchive: true
                    mail (
                        subject: "Security Scan FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Security scan failed. Logs can be downloaded from: ${env.BUILD_URL}artifact/security-scan.log",
                        to: "${env.EMAIL_RECIPIENTS}"
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to staging (e.g., AWS EC2 instance)...'
                echo 'Tool: AWS CLI'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests in the staging environment...'
                echo 'Tool: Selenium for testing'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to production (e.g., AWS EC2 instance)...'
                echo 'Tool: AWS CLI'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '*.log', allowEmptyArchive: true
        }

        success {
            mail (
                subject: "SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                body: "Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] succeeded. Logs can be downloaded from: ${env.BUILD_URL}artifact/*.log",
                to: "${env.EMAIL_RECIPIENTS}"
            )
        }

        failure {
            mail (
                subject: "FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                body: "Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] failed. Logs can be downloaded from: ${env.BUILD_URL}artifact/*.log",
                to: "${env.EMAIL_RECIPIENTS}"
            )
        }
    }
}
