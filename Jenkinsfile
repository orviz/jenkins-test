pipeline {
    agent none

    //triggers {
    //    pollSCM('H/15 * * * *')
    //}


    stages {
        stage('Properties') {
			steps {
                script {
                    properties([
                        pipelineTriggers([
                            [$class: "GitHubPushTrigger"]
                        ])
                    ])
                }
                echo 'Environment step'
            }
        }
        stage('Build') {
            parallel {
                stage('Build on Ubuntu16.04') {
                    properties([pipelineTriggers([[$class: 'GitHubPushTrigger'], pollSCM('H/15 * * * *')])])
                    agent {
                        label 'bubuntu16'
                    }
                    steps {
						script {
                            properties([
                                pipelineTriggers([
                                    [$class: "GitHubPushTrigger"]
                                ])
                            ])
                        }
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
                            archiveArtifacts artifacts: '**/debs/*.deb'                        }
                    }
                }
                stage('Build on CentOS7') {
                    agent {
                        label 'bcentos7'
                    }
                    steps {
                        echo 'Within build on CentOS7'
                        sh 'git clone https://github.com/EGI-Foundation/cloud-info-provider'
                        
                        dir("${WORKSPACE}/cloud-info-provider") {
                            sh 'sudo yum install -y rpm-build centos-release-openstack-newton python-pbr python-setuptools'
                            sh 'python setup.py sdist'
                            sh 'mkdir ~/rpmbuild'
                            sh "echo '%_topdir %(echo $HOME)/rpmbuild' > ~/.rpmmacros"
                            sh 'mkdir -p ~/rpmbuild/{SOURCES,SPECS}'
                            sh 'cp dist/cloud_info_provider*.tar.gz ~/rpmbuild/SOURCES/'
                            sh 'cp rpm/cloud-info-provider*.spec ~/rpmbuild/SPECS/'
                            //sh 'rpmbuild -ba ~/rpmbuild/SPECS/cloud-info-provider.spec'
                            sh 'rpmbuild -ba ~/rpmbuild/SPECS/cloud-info-provider-openstack.spec'
                            sh 'rpmbuild -ba ~/rpmbuild/SPECS/cloud-info-provider-opennebula.spec'
                            sh 'cp ~/rpmbuild/SRPMS/*.rpm ~/rpmbuild/RPMS/noarch/*.rpm ${WORKSPACE}/cloud-info-provider/rpm/'                        }
                    }
                    post {
                        success {
                            archiveArtifacts artifacts: '**/rpm/*.rpm'
                        }
                    }
                }
            }
        }
    }
}
