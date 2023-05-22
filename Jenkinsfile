#!/usr/bin/env groovy
pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("increment version") {
            steps {
                script {
                    echo "incrementing app version..."
                    sh 'mvn build-helper:parse-version versions:set \
                        -DnewVersion=\\\${parsedVersion.majorVersion}.\\\${parsedVersion.minorVersion}.\\\${parsedVersion.nextIncrementalVersion} \
                        versions:commit'
                    def matcher = readFile('pom.xml') =~ '<version>(.+)</version>'
                    def version = matcher[0][1]
                    env.IMAGE_NAME = "$version-$BUILD_NUMBER"
                }
            }
        }
        stage('build app') {
            steps {
                script {
                    echo "building the application..."
                    sh 'mvn clean package'
                }
            }
        }
        stage("build image") {
            steps {
                script {
                    echo "building the docker image."
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-repo', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh "docker build -t qw1qw123/demo-app:${IMAGE_NAME} ."
                        sh "echo $PASS | docker login -u $USER --password-stdin"
                        sh "docker push qw1qw123/demo-app:${IMAGE_NAME}"
                    }
                }
            }
        }    
        stage("deploy") {
            steps {
                script {
                    echo 'deploying the application...'
                }
            }
        }
        stage('commit version update') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'github-credential', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                        sh 'git config user.email "kornzhou0602@gmail.com"'
                        sh 'git config user.name "korn"'

                        sh 'git status'
                        sh 'git branch'
                        sh 'git config --list'

                        sh "git remote set-url orgin https://${USER}:${PASS}@github.com/kornzhoudev/jenkins-app.git"
                        sh 'git add .'
                        sh 'git commit -m "ci: version bump${BUILD_NUMBER}"'
                        sh 'git push orgin HEAD:jenkins-jobs'
                    }
                }
            }
        }
    }
}
