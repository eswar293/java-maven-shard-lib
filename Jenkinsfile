#! /user/bin/env groovy

@Library('Jenkins-shared-library')

def gv

pipeline {   
    agent any
    tools {
        maven 'maven3.9'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("build jar") {
            steps {
                script {
                  buildjar()
                }
            }
        }
        \\ adding this branch
        stage("build image") {
            steps {
                script {
                    buildImage 'eswar1241/my-repo:jma-2.0'
                }
            }
        }

        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
            post {
                success {
                    echo "installed dependences bild libraries and build docker iamge sucessfully"
                }
                failure {
                    echo "Failed at $BRNACH_NAME"
                }
            }
        }
                       
    }
} 
