pipeline {
    agent none
    stages {
        stage("test") {
            steps {
                script {
                    echo "Testing the application..."
                    echo "Execting pipeline for brach $BRANCH_NAME"
            }
        }
        stage("build") {
            when {
                expression {
                    BRANCH_NAME == 'main'
                }
            }
            steps {
                script {
                    echo "1"
                }
            }
        }
        stage("deploy") {
            when {
                expression {
                    BRANCH_NAME == 'main'
                }
            }
            steps {
                script {
                    echo "2"
                }
            }
        }
    }   
}
