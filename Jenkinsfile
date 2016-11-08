#!groovy


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


def check_source{
    checkout scm
}

def unit_tests{
    sh 'cd src'
    sh 'sudo make --warn-undefined-variables test_valgrind'
    sh 'sudo make clean'
}

for (x in labels) {
    def label = x

    node(label) {
        stage ('Checkout source'){
            check_source()
        }
        stage ('Unit Tests'){
            unit_tests()
        }
    }
}
