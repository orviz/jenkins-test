#!groovy

pipeline {
    agent {
        node {
            label 'bubuntu16'
        }
    }

    environment {
        WORKWTF = pwd()
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'git clone https://github.com/EGI-Foundation/cloud-info-provider'

                dir("${WORKSPACE}/cloud-info-provider") {
                    sh 'sudo apt-get update && sudo apt-get install -y devscripts debhelper python-all-dev python-pbr python-setuptools'
                    sh 'debuild --no-tgz-check clean binary'
                }
                dir("${WORKSPACE}/cloud-info-provider/debs/cloud-info-provider-openstack") {
                    sh 'debuild --no-tgz-check clean binary'
                }
                dir("${WORKSPACE}/cloud-info-provider/debs/cloud-info-provider-opennebula") {
                    sh 'debuild --no-tgz-check clean binary'
                }
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: '**/debs/*.deb'
        }
    }                          
}
