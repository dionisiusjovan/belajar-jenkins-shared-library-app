pipeline {
    /*
    agent {
        node {
            label "java11 && linux"
        }
    }
    */
    agent none

    environment {
        WEBHOOK_URL = credentials("DISCORD_WEBHOOK_URL")
    }

    stages {
        stage("Prepare") {
            agent {
                node {
                    label "java11 && linux"
                }
            }
            steps {
                echo "Discord Webhook URL: ${WEBHOOK_URL}"
                echo "Start Job: ${env.JOB_NAME}"
                echo "Start Build: ${env.BUILD_NUMBER}"
                echo "Branch Name: ${env.BRANCH_NAME}"
            }
        }

        stage("Build") {
            agent {
                node {
                    label "java11 && linux"
                }
            }
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
            agent {
                node {
                    label "java11 && linux"
                }
            }
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
            agent {
                node {
                    label "java11 && linux"
                }
            }
            steps {
                echo "Hello Deploy"
            }
        }
    }

    post {
        always {
            echo "Send notification to discord"

            discordSend link: env.BUILD_URL, 
                        result: currentBuild.description, 
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