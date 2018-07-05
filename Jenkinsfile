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
                //dir('/tmp/cloud-info-provider') {
                dir('cloud-info-provider') {
                    sh 'sudo apt-get update && sudo apt-get install -y devscripts debhelper python-all-dev python-pbr python-setuptools'
                    sh 'debuild --no-tgz-check clean binary'
                }
                //dir('/tmp/cloud-info-provider/debs/cloud-info-provider-openstack') {
                //    sh 'debuild --no-tgz-check clean binary'
                //}
                //dir('/tmp/cloud-info-provider/debs/cloud-info-provider-opennebula') {
                //    sh 'debuild --no-tgz-check clean binary'
                //}
                //dir('/tmp/cloud-info-provider') {
                //    sh 'find | grep deb'
                //}

            }
        }
    }

    //post {
    //    success {
    //        archiveArtifacts artifacts: '/tmp/cloud-info-provider/debs/*.deb'
    //    }
    //}                          
}
