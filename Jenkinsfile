pipeline {
    agent any
    
    stages {
        stage('Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/prakash1330/Jenkins_Webhook_test.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'chmod +x ./Test.sh'  // Grant execute permission
                sh './Test.sh'  // Execute the script
            }
        }
        
        stage('Test') {
            steps {
                echo "This is Test Stage"
            }
        }
        
        stage('Deployment') {
            steps {
                echo "This is Deployment Stage"
            }
        }
    }
    
    post {
        success {
            script {
                echo "Sending success email..."
            }
            emailext (
                subject: "Jenkins Build Success: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    Build ${env.JOB_NAME} #${env.BUILD_NUMBER} was successful.

                    Here's a summary of the output:
                    
                    ${currentBuild.currentResult}

                    Full logs: ${env.BUILD_URL}/console
                """,
                attachLog: true,
                to: 'pp0485322@gmail.com'
            )
        }
        failure {
            script {
                echo "Sending failure email..."
            }
            emailext (
                subject: "Jenkins Build Failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """
                    Build ${env.JOB_NAME} #${env.BUILD_NUMBER} failed.

                    Here's a summary of the output:

                    ${currentBuild.currentResult}

                    Full logs: ${env.BUILD_URL}/console
                """,
                attachLog: true,
                to: 'pp0485322@gmail.com'
            )
        }
    }
}
