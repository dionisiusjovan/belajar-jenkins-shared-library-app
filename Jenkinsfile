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
                script {
                    for (int i = 0; i < 10; i++) {
                        echo "Script ${i}"
                    }
                }

                echo "Start Build"
                sh("./mvnw clean compile test-compile")
                echo "Finish Build"
            }
        }
        stage("Test") {
            steps {
                script {
                    def data = [
                        "firstName": "Eko", "lastName": "Khannedy"
                    ]
                    writeJSON(file: "data.json", json: data)
                }


                echo "Hello Test"
                sh("./mvnw test")
                /* sh("error") */
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