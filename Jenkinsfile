#!groovy

pipeline {
    //agent {
    //    node {
    //        label 'bubuntu16'
    //    }
    //}
    agent none

    stages {
        stage('Build') {
            steps {
                node('bubuntu16') {
                    echo 'Building DEBs on Ubuntu 16.06..'
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

                node('bcentos7') {
                    echo 'Building RPMs on CentOS7..'
                    sh 'git clone https://github.com/EGI-Foundation/cloud-info-provider'
                }
            }
        }
    }

    //post {
    //    success {
    //        archiveArtifacts artifacts: '**/debs/*.deb'
    //    }
    //}                          
}
