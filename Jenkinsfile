#!groovy

//node {
//    checkout scm
    agent {
        docker.withServer('tcp://172.16.39.13:2375') {
            docker.image('indigodatacloud/ci-images:python')
        }
    }
pipeline {
    stages {
        stage('Build') {
            echo 'Building..'
        }
        stage('Test') {
            echo 'Testing..'
        }
        stage('Deploy') {
            echo 'Deploying....'
        }
    }
}
