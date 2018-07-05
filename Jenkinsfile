#!groovy

pipeline {
    agent none

    stages {
        stage('Build') {
    //        steps {
                parallel ubuntu: {
                    node('bubuntu16') {
                        stage {
                            steps {
                                echo 'Building DEBs on Ubuntu 16.06..'
                            }
                        }
                        //post {
                        //    success {
                        //        //archiveArtifacts artifacts: '**/debs/*.deb'
                        //    }
                        //}                          
                    }
                },
                centos: {
                    node('bcentos7') {
                        echo 'Building RPMs on CentOS7..'
    //                    sh 'git clone https://github.com/EGI-Foundation/cloud-info-provider'
                    }
                }
    //        }
        }
    }
}
