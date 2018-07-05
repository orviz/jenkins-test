#!groovy

pipeline {
    agent none

    stages {
        stage('Build') {
            parallel {
                stage('Build on Ubuntu16.04') {
                    agent {
                        label 'bubuntu16'
                    }
                    steps {
                        echo 'Within build on Ubuntu16.04'   
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
                    post {
                        success {
                            archiveArtifacts artifacts: '**/debs/*.deb'
                        }
                    }
                }
                stage('Build on CentOS7') {
                    agent {
                        label 'bcentos7'
                    }
                    steps {
                        echo 'Within build on CentOS7'    
                    }
                    post {
                        success {
                            echo "post-build here"
                        }
                    }
                }
            }
        }
    }
}
