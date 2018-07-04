#!groovy

node {
    checkout scm

    docker.withServer('tcp://172.16.39.13:2375') {
        docker.image('indigodatacloud/ci-images:python')
    }

    stage('Build') {
        step {
            echo 'Building..'
        }
    }
    stage('Test') {
        step {
            echo 'Testing..'
        }
    }
    stage('Deploy') {
        step {
            echo 'Deploying....'
        }
    }
}
