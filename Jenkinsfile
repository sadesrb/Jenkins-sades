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
                // Replace with Windows-friendly build command if applicable
                bat 'echo "Simulating Maven Build in Windows" > build.log'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit tests with JUnit and integration tests...'
                echo 'Tools: JUnit for unit tests, TestNG for integration tests'
                // Example command to simulate test log creation on Windows
                bat 'echo "Running Unit and Integration Tests" > unit_integration_test.log'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'unit_integration_test.log', allowEmptyArchive: true
                    emailext (
                        subject: "Unit and Integration Tests SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Unit and integration tests passed successfully.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachmentsPattern: 'unit_integration_test.log'
                    )
                }
                failure {
                    archiveArtifacts artifacts: 'unit_integration_test.log', allowEmptyArchive: true
                    emailext (
                        subject: "Unit and Integration Tests FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Unit and integration tests failed. Please check the logs.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachmentsPattern: 'unit_integration_test.log'
                    )
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis with SonarQube...'
                echo 'Tool: SonarQube'
                // Simulating code analysis log creation on Windows
                bat 'echo "Performing Code Analysis" > code_analysis.log'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'code_analysis.log', allowEmptyArchive: true
                    emailext (
                        subject: "Code Analysis SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Code analysis passed successfully.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachmentsPattern: 'code_analysis.log'
                    )
                }
                failure {
                    archiveArtifacts artifacts: 'code_analysis.log', allowEmptyArchive: true
                    emailext (
                        subject: "Code Analysis FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Code analysis failed. Please check the logs.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachmentsPattern: 'code_analysis.log'
                    )
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan using OWASP Dependency-Check...'
                echo 'Tool: OWASP Dependency-Check'
                // Simulate security scan log creation on Windows
                bat 'echo "Running Security Scan" > security_scan.log'
            }
            post {
                success {
                    archiveArtifacts artifacts: 'security_scan.log', allowEmptyArchive: true
                    emailext (
                        subject: "Security Scan SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Security scan passed successfully.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachmentsPattern: 'security_scan.log'
                    )
                }
                failure {
                    archiveArtifacts artifacts: 'security_scan.log', allowEmptyArchive: true
                    emailext (
                        subject: "Security Scan FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                        body: "Security scan failed. Please check the logs.",
                        to: "${env.EMAIL_RECIPIENTS}",
                        attachmentsPattern: 'security_scan.log'
                    )
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying the application to staging (e.g., AWS EC2 instance)...'
                echo 'Tool: AWS CLI'
                // Simulating deployment step on Windows
                bat 'echo "Deploying to Staging" > deploy_staging.log'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests in the staging environment...'
                echo 'Tool: Selenium for testing'
                // Simulate log creation for tests on staging
                bat 'echo "Running Integration Tests on Staging" > integration_staging_test.log'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying the application to production (e.g., AWS EC2 instance)...'
                echo 'Tool: AWS CLI'
                // Simulate production deployment log creation
                bat 'echo "Deploying to Production" > deploy_production.log'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '/*.log', allowEmptyArchive: true
        }

        success {
            emailext (
                subject: "SUCCESS: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                body: "Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] succeeded.",
                to: "${env.EMAIL_RECIPIENTS}",
                attachmentsPattern: '/*.log'  // Attach all log files
            )
        }

        failure {
            emailext (
                subject: "FAILURE: Jenkins Job ${env.JOB_NAME} [${env.BUILD_NUMBER}]",
                body: "Job ${env.JOB_NAME} [${env.BUILD_NUMBER}] failed. Please check the logs.",
                to: "${env.EMAIL_RECIPIENTS}",
                attachmentsPattern: '/*.log'  // Attach all log files
            )
        }
    }
}
