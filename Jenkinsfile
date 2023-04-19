pipeline {
    agent {
        node {
            label "java11 && linux"
        }
    }

    stages {
        stage("Hello") {
            steps {
                echo "Hello Pipeline"
            }
        }
    }

    post {
        always {
            echo "Send notification to discord"
            discordSend description: "Jenkins Pipeline Build", 
                        link: env.BUILD_URL, 
                        result: currentBuild.currentResult, 
                        title: JOB_NAME, 
                        webhookURL: "https://discord.com/api/webhooks/1097057271076364328/OmDZQ6TA-mnXD-9JTXoY0zOFerAjWZLFvpCBcQGMnrReDzX7M3SbO-0gduZf0difRHE8"
        }
        always {
            mail to: "dionisiusplayground@gmail.com",
            subject: JOB_NAME
        }
        success {
            echo "success"
        }
        failure {
            echo "failed"
        }
        cleanup {
            echo "Don't care success or failed"
        }

    }
}