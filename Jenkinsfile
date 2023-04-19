pipeline {
    agent {
        node {
            label "java11 && linux"
        }
    }

    environment {
        WEBHOOK_URL = "https://discord.com/api/webhooks/1097057271076364328/OmDZQ6TA-mnXD-9JTXoY0zOFerAjWZLFvpCBcQGMnrReDzX7M3SbO-0gduZf0difRHE8"
    }

    stages {
        stage("Build") {
            steps {
                echo "Hello Build"
            }
        }
        stage("Test") {
            steps {
                echo "Hello Test"
            }
        }
        stage("Deploy") {
            steps {
                echo "Hello Deploy"
            }
        }
    }

    post {
        always {
            echo "Send notification to discord"

            discordSend link: env.BUILD_URL, 
                        result: currentBuild.currentResult, 
                        title: JOB_NAME, 
                        webhookURL: WEBHOOK_URL,
                        description: "**Build:** ${env.BUILD_NUMBER}\n**Status:** ${currentBuild.currentResult.toLowerCase()}\n\u2060", /* word joiner character forces a blank line */
                        enableArtifactsList: true,
                        showChangeset: true

            /* 
            mail to: "dionisiusplayground@gmail.com",
                 subject: JOB_NAME,
                 body: currentBuild.currentResult
            */
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