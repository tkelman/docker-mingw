# Dockerfile for testing Centos 5 with the devtoolset-2
FROM centos:5
MAINTAINER Tony Kelman <tony@kelman.net>

RUN yum install wget epel-release -y
RUN wget -O /etc/yum.repos.d/slc5-devtoolset.repo http://linuxsoft.cern.ch/cern/devtoolset/slc5-devtoolset.repo
RUN yum install devtoolset-2 bzip2 python26 git m4 patch cmake -y --nogpgcheck
