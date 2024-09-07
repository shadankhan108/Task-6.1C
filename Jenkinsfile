pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Build succeeded.'
                }
                failure {
                    echo 'Build failed.'
                    // Add actions to handle build failure, e.g., notifying team
                }
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                sh 'mvn test'
            }
            post {
                success {
                    echo 'Tests succeeded.'
                }
                failure {
                    echo 'Tests failed.'
                    // Add actions to handle test failure
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis...'
                withSonarQubeEnv('SonarQube') {
                    sh 'mvn sonar:sonar'
                }
            }
            post {
                success {
                    echo 'Code analysis completed.'
                }
                failure {
                    echo 'Code analysis failed.'
                    // Add actions to handle code analysis failure
                }
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan...'
                sh 'dependency-check.sh --project myapp --scan .'
            }
            post {
                success {
                    echo 'Security scan completed.'
                }
                failure {
                    echo 'Security scan failed.'
                    // Add actions to handle security scan failure
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo 'Deploying to staging environment...'
                sh 'aws deploy push --application-name my-app-staging --s3-location s3://my-bucket/my-app-staging.zip'
            }
            post {
                success {
                    echo 'Deployment to staging succeeded.'
                }
                failure {
                    echo 'Deployment to staging failed.'
                    // Add actions to handle deployment failure
                }
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging...'
                sh 'mvn verify'
            }
            post {
                success {
                    echo 'Integration tests succeeded.'
                }
                failure {
                    echo 'Integration tests failed.'
                    // Add actions to handle integration test failure
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                echo 'Deploying to production environment...'
                sh 'aws deploy push --application-name my-app-prod --s3-location s3://my-bucket/my-app-prod.zip'
            }
            post {
                success {
                    echo 'Deployment to production succeeded.'
                }
                failure {
                    echo 'Deployment to production failed.'
                    // Add actions to handle deployment failure
                }
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
