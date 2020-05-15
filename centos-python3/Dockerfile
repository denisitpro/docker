FROM centos:7

RUN yum remove git -y && \
    yum update -y && \
    yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo && \
    yum install -y  https://centos7.iuscommunity.org/ius-release.rpm && \
    yum install -y gcc gcc-c++ \
                   libtool libtool-ltdl \
                   make cmake \
                   git2u-all \
                   curl \
                   wget \
                   rsync \
                   yum-utils device-mapper-persistent-data lvm2 \
                   pkgconfig \
                   sudo \
                   automake autoconf \
                   docker-ce \
                   docker-ce-cli \
                   openssl-devel \
                   bzip2-devel \
                   libffi-devel \
                   yum-utils \
                   rpm-build && \
    yum clean all

RUN wget https://www.python.org/ftp/python/3.7.7/Python-3.7.7.tgz && \
    tar xzf Python-3.7.7.tgz && \
    Python-3.7.7/configure --enable-optimizations && \
    make altinstall && \
    rm -rf Python-3.7.7 && \
    rm -f Python-3.7.7.tgz

RUN useradd builder -u 1000 -m -G users,wheel && \
    echo "builder ALL=(ALL:ALL) NOPASSWD:ALL" >> /etc/sudoers && \
    echo "# macros"                      >  /home/builder/.rpmmacros && \
    echo "%_topdir    /home/builder/rpm" >> /home/builder/.rpmmacros && \
    echo "%_sourcedir %{_topdir}"        >> /home/builder/.rpmmacros && \
    echo "%_builddir  %{_topdir}"        >> /home/builder/.rpmmacros && \
    echo "%_specdir   %{_topdir}"        >> /home/builder/.rpmmacros && \
    echo "%_rpmdir    %{_topdir}"        >> /home/builder/.rpmmacros && \
    echo "%_srcrpmdir %{_topdir}"        >> /home/builder/.rpmmacros && \
    mkdir /home/builder/rpm && \
    chown -R builder /home/builder
USER builder

ENV FLAVOR=rpmbuild OS=centos DIST=el7
CMD /srv/pkg