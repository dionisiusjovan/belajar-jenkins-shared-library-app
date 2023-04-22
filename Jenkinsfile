@Library("belajar-jenkins-shared-library@master") _

import programmerzamannow.jenkins.Output

pipeline {
    agent any
    stages {
        stage ("Global Variable") {
            steps {
                script {
                    echo author()
                    echo author.name()
                    echo author.channel()
                }
            }
        }
        stage ("Execute Maven") {
            steps {
                script {
                    maven('clean compile')
                }
            }
        }
        /*
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
        stage ("Hello Groovy Steps") {
            steps {
                script {
                    Output.hello_param(this, "Groovy Steps")
                }
            }
        }
        */
    }
}