/**
 * Jenkinsfile for OSSEC Wazuh
 * Copyright (C) 2016 Wazuh Inc.
 * June 22, 2016.
 *
 * This program is a free software; you can redistribute it
 * and/or modify it under the terms of the GNU General Public
 * License (version 2) as published by the FSF - Free Software
 * Foundation.
 */


def labels = ['ubuntu-xenial-slave', 'ubuntu-trusty-slave', 'centos-7-slave', 'debian-8-slave', 'debian-7-slave']


def stage1(){
    checkout scm
    sh 'sudo apt-get update'
    sh 'ls -l'
}

def stage2(){
    sh 'cd src'
    sh 'ls -l'
    sh 'sudo make --warn-undefined-variables test_valgrind'
    sh 'sudo make clean'
}

for (x in labels) {
    def label = x

    stage (label){
        node(label) {
            stage ('Checkout source'){
                stage1()
            }
            stage ('Unit Tests'){
                stage2()
            }
        }
    }
}
