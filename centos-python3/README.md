# CentOS 7 and python 3
This docker image can be used to build RPM packages. Fork  https://hub.docker.com/r/rpmbuild/centos7/

## Change for me
* install python 3.7.7
* Add support docker-ce 

## Third-Party Repositories.
docker-ce.repo

## Installed Software
Aside from the additions to make a baseline kit (sudo, git, etc.), the following software is loaded:

autoconf / libtool / devscripts
* Python-3.7.7
* pkgconfig
* yum-utils
* rpm-build
* curl
* wget
* docker-ce
* docker-ce-cli
* and etc

## Hook / Integration
When running this container, you will need to provide a /srv mountpoint, which must contain, at its root, a pkg script that is executable. The image will execute this build script to perform the actual packaging (including installation of dependencies, running of tests, debuild calls, etc.)

RPMs will be built in /home/builder/rpm, which should contain source archives, patches and built RPM/SRPM files.
