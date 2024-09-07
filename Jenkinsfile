pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                // Clean and package the project using Maven
                sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                // Run tests using Maven
                sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                // Run SonarQube analysis
                withSonarQubeEnv('SonarQube') { // Ensure 'SonarQube' matches your SonarQube configuration
                    sh 'mvn sonar:sonar'
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                // Run OWASP Dependency-Check (make sure the script and flags are correct)
                sh 'dependency-check.sh --project myapp --scan .'
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                // Use AWS CLI for staging deployment
                sh 'aws deploy push --application-name my-app-staging --s3-location s3://my-bucket/my-app-staging.zip'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                // Run integration tests using Maven
                sh 'mvn verify'
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                // Use AWS CLI for production deployment
                sh 'aws deploy push --application-name my-app-prod --s3-location s3://my-bucket/my-app-prod.zip'
            }
        }
    }

    post {
        always {
            mail to: 'shadankhan108@gmail.com',
                 subject: "Pipeline Status: ${currentBuild.currentResult}",
                 body: "The pipeline finished with status: ${currentBuild.currentResult}. Check the Jenkins logs for details."
        }
    }
}
