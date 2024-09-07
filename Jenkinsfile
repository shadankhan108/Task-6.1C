pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the code using Maven...'
                // Example: sh 'mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo 'Running Unit and Integration Tests using JUnit...'
                // Example: sh 'mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo 'Running Code Analysis using SonarQube...'
                // Example: sh 'sonar-scanner'
            }
        }
        stage('Security Scan') {
            steps {
                echo 'Running Security Scan using OWASP Dependency-Check...'
                // Example: sh 'dependency-check --project JenkinsPipeline --scan ./'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to Staging using AWS CLI...'
                // Example: sh 'aws deploy ...'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo 'Running Integration Tests on Staging using Postman/Newman...'
                // Example: sh 'newman run collection.json'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo 'Deploying to Production using AWS CLI...'
                // Example: sh 'aws deploy ...'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline finished!'
        }
        failure {
            script {
                emailext(
                    to: 'shadankhan108@gmail.com',
                    subject: "Jenkins Build Failed: ${env.BUILD_ID}",
                    body: """<p>Build ${env.BUILD_ID} failed. Check Jenkins for details.</p>
                             <p>Console output: <a href="${env.BUILD_URL}console">${env.BUILD_URL}console</a></p>""",
                    attachLog: true
                )
            }
        }
        success {
            script {
                emailext(
                    to: 'shadankhan108@gmail.com',
                    subject: "Jenkins Build Success: ${env.BUILD_ID}",
                    body: """<p>Build ${env.BUILD_ID} completed successfully.</p>
                             <p>Console output: <a href="${env.BUILD_URL}console">${env.BUILD_URL}console</a></p>""",
                    attachLog: true
                )
            }
        }
    }
}
