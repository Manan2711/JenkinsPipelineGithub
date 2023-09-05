pipeline{
    agent any

    environment{
        BUILD_TOOL = "Maven"

        UNIT_TEST_TOOL = "JUnit" 
        //UNIT_TEST_TOOL = "TestNG" 
        
        CODE_ANALYSIS_TOOL = "SonarQube"
        
        SECURITY_SCAN_TOOL = "OWASP ZAP"
        
        DEPLOYMENT_TOOL = "AWS EC2"
    }

    stages {
        stage("Build") {
            steps {
                echo "Using build automation tool: $BUILD_TOOL"
            }
        }

        stage("Unit and Integration Tests") {
            steps {
                echo "Using test automation tools: $UNIT_TEST_TOOL"
                echo "Running integration tests"
            }
            post {
                success {
                    emailext attachLog: true,
                    body: "Testing Status - ${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                    to: "sit223task@gmail.com",
                    subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
                }
                failure {
                    emailext attachLog: true,
                    body: "$Testing Status - {currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                    to: "sit223task@gmail.com",
                    subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
                }
            }
        }

        stage("Code Analysis") {
            steps {
                echo "Using code analysis tool: $CODE_ANALYSIS_TOOL"
            }
        }

        stage("Security Scan") {
            steps {
                echo "Using security scanning tool: $SECURITY_SCAN_TOOL"
            }

            post {
                success {
                    emailext attachLog: true,
                    body: "Security Scan Status - ${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                    to: "sit223task@gmail.com",
                    subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
                }
                failure {
                    emailext attachLog: true,
                    body: "Security Scan Status - ${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                    to: "sit223task@gmail.com",
                    subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
                }
            }
        }

        stage("Deploy to Staging") {
            steps {
                echo "Deploying to staging environment: $DEPLOYMENT_TOOL"
            }
        }

        stage("Integration Tests on Staging") {
            steps {
                echo "Running tests on staging environment"
            }
        }

        stage("Deploy to Production") {
            steps {
                echo "Deploying to production environment: $DEPLOYMENT_TOOL"
            }
        }
    }
}