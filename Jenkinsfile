@Library("belajar-jenkins-shared-library@master") _

import programmerzamannow.jenkins.Output

pipeline {
    agent any
    stages {
        stage ("Hello World") {
            steps {
                script {
                    hello.world()
                }
            }
        }
        stage ("Hello Groovy") {
            steps {
                script {
                    Output.hello("Groovy")
                }
            }
        }
    }
}