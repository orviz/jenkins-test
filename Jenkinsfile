#!groovy

pipeline {
    //agent any
    agent {
        checkout scm

        node {
            docker.withServer('tcp://172.16.39.13:2375', '') {
                docker.image('indigodatacloud/ci-images:python')
            }
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
