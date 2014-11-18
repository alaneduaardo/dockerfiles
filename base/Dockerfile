################################################################
# Creates a base CentOS 6.5 image with Developer tools
#
#                    ##        .
#              ## ## ##       ==
#           ## ## ## ##      ===
#       /""""""""""""""""\___/ ===
#  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
#       \______ o          __/
#         \    \        __/
#          \____\______/
#
# Author:    Alan Eduardo <alan_eduardo@outlook.com.br>
# License:   MIT
#################################################################

FROM tianon/centos:6.5
MAINTAINER Alan Eduardo <alan_eduardo@outlook.com.br>

ENV SERF_SERVER 172.17.42.1
EXPOSE 22

ENV LANG       pt_BR.UTF-8
ENV LC_ALL     pt_BR.UTF-8

# add epel repo
RUN rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm

# update
RUN yum -y update
RUN yum clean all && yum -y upgrade && yum clean all

# install base packages
RUN yum -y groupinstall "Development Tools"
RUN yum -y install gcc gcc-c++ kernel-devel-`uname -r` make perl sqlite-devel bzip2 bzip2-devel zlib-devel ncurses-devel readline-devel tk-devel net-tools nfs-utils openssl-devel git screen tmux wget zsh htop vim

# fix paths
RUN echo 'Defaults  secure_path=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin' >> /etc/sudoers.d

# ssh key
ADD id_rsa.pub /root/.ssh/authorized_keys
RUN chown -R root. /root/.ssh

CMD [ "/usr/bin/supervisord", "-c", "/etc/supervisord.conf" ]

ADD src/ /tmp/src/
RUN /tmp/src/setup.sh
