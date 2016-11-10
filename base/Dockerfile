FROM openshift/base-centos7
MAINTAINER Tobias Florek <tob@butter.sh>
USER 0
ENV BAREOS_HOME=/var/lib/bareos \
    BAREOS_UID=997

ADD entrypoint.sh /usr/libexec/container-scripts/
ENTRYPOINT /usr/libexec/container-scripts/entrypoint.sh

RUN curl -Lo /etc/yum.repos.d/bareos.repo http://download.bareos.org/bareos/release/16.2/CentOS_7/bareos.repo \
 && curl -Lo /etc/pki/rpm-gpg/RPM-GPG-KEY-bareos http://download.bareos.org/bareos/release/16.2/CentOS_7/repodata/repomd.xml.key \
 && test $(HOME=/tmp gpg --with-fingerprint /etc/pki/rpm-gpg/RPM-GPG-KEY-bareos | grep Key\ fingerprint | sed 's/ //g'| cut -f2 -d=) = 0143857D9CE8C2D182FE2631F93C028C093BFBA2 \
 && rpmkeys --import /etc/pki/rpm-gpg/RPM-GPG-KEY-bareos \
 && sed -i 's_gpgkey=.*_gpgkey=file:///etc/pky/rpm-gpg/RPM-GPG-KEY-bareos_' /etc/yum.repos.d/bareos.repo \
 && yum -y install bareos-common \
 && yum clean all \
 && chmod -R a+rwX $BAREOS_HOME /etc/bareos

# override home for bareos user
ENV HOME=/var/lib/bareos
