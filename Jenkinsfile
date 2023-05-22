pipeline {
    agent any
    stages {
        stage("test") {
            steps {
                script {
                    echo "Testing the app..."
                    echo "Executing pipepline for branch $Branch_NAME"
                }
            }
        }
        stage("build image") {
            when {
                expression {
                    branch = 'main'
                }
            }
            steps {
                script {
                    echo "Building the app.."
                }
            }
        }
        stage("deploy") {
            when {
                expression {
                    branch = 'main'
                }
            }
            steps {
                script {
                    echo "deploy the app.."
                }
            }
        }
    }
}
