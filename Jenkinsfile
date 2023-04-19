pipeline {
    agent {
        node {
            label {
                "java11 && linux"
            }
        }
    }

    stages {
        stage("Hello") {
            steps {
                echo "Hello Pipeline"
            }
        }
    }
}