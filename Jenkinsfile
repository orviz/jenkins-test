#!groovy

pipeline {
    agent {
        node {
            label 'bubuntu16'
        }
    }
    
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'git clone https://github.com/EGI-Foundation/cloud-info-provider /tmp/cloud-info-provider'
                dir('/tmp/cloud-info-provider') {
                    sh 'pwd'
                }
            }
        }
                                        
    }
}
