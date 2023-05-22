pipeline {
    agent any
    tools {
        maven 'Maven'
    }
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
                    BRANCH_NAME = 'main'
                }
            }
            steps {
                script {
                    echo "Building the application..."
                }
            }
        }
        stage("deploy") {
            when {
                expression {
                    BRANCH_NAME = 'main'
                }
            }
            steps {
                script {
                    echo "deploy the application.."
                }
            }
        }
    }
}
