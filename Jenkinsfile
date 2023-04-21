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

    // triggers {
        // cron("*/5 * * * *")
        // pollSCM("*/5 * * * *")
        // upstream(upstreamProjects: 'job1, job2', threshold: hudson.model.Result.SUCCESS)
    // }

    options {
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your Name?")
        text(name: "DESCP", defaultValue: "", description: "Tell us about you?")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which Social Media?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt key")
    }

    stages {
        stage("Preparation") {
            agent {
                node {
                    label "java11 && linux"
                }
            }
            stages {
                stage("Prepare Java") {
                    steps {
                        echo "Loading Java"
                    }
                }
                stage("Prepare Maven") {
                    steps {
                        echo "Loading Maven"
                    }
                }
            }
        }

        stage("Prepare") {
            agent {
                node {
                    label "java11 && linux"
                }
            }
            steps {
                sh('echo "Discord Webhook URL: $WEBHOOK_URL" > "webhook_url.txt"')
                echo "Start Job: ${env.JOB_NAME}"
                echo "Start Build: ${env.BUILD_NUMBER}"
                echo "Branch Name: ${env.BRANCH_NAME}"
            }
        }

        stage("Parameters") {
            agent {
                node {
                    label "java11 && linux"
                }
            }
            steps {
                echo "Hello ${params.NAME}"
                echo "Descp: ${params.DESCP}"
                echo "Choice: ${params.SOCIAL_MEDIA}"
                echo "Deploy: ${params.DEPLOY}"
                echo "Secret Key: ${params.SECRET}"
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
            input {
                message "Can we deploy?"
                ok "Yes"
                submitter "admin"
                parameters {
                    choice(name: "TARGET_ENV", choices: ['DEV', 'QA', 'PROD'], description: "Which ENV?")
                }
            }
            steps {
                echo "DEPLOYING TO ${TARGET_ENV}"
                echo "Hello Deploy"
            }
        }
        stage("Release") {
            when {
                expression {
                    return params.DEPLOY
                }
            }

            agent {
                node {
                    label "java11 && linux"
                }
            }
            steps {
                echo "Release"
            }
        }
    }

    post {
        always {
            echo "Send notification to discord"

            discordSend link: env.BUILD_URL, 
                        result: currentBuild.description, 
                        title: JOB_NAME, 
                        webhookURL: "https://discord.com/api/webhooks/1097057271076364328/OmDZQ6TA-mnXD-9JTXoY0zOFerAjWZLFvpCBcQGMnrReDzX7M3SbO-0gduZf0difRHE8",
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