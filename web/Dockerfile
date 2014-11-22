FROM alaneduaardo/base
MAINTAINER Alan Eduardo <alan_eduardo@outlook.com.br>

EXPOSE 80
ENV ROLE web

#repos for the hhvm installation
RUN rpm -Uvh http://dheche.fedorapeople.org/hhvm/el6/RPMS/x86_64/hhvm-release-6-1.noarch.rpm

# install nginx php and tools to compile phalcon
RUN yum -y --nogpgcheck install nginx php-fpm php-devel pcre-devel gcc make php-pdo php-mysql php-pgsql hhvm

# Compile Phalcon
RUN git clone --depth=1 git://github.com/phalcon/cphalcon.git /root/cphalcon
RUN cd /root/cphalcon/build && ./install 64bits
RUN echo "extension=phalcon.so" >> /etc/php.d/phalcon.ini

# Server Configuration Files
ADD default.conf /etc/nginx/conf.d/default.conf
ADD php.ini /etc/php.ini
ADD www.conf /etc/php-fpm.d/www.conf

# Sites Configuration Files

# Init Servers
RUN chkconfig nginx on
RUN chkconfig php-fpm on
RUN service nginx restart
RUN service php-fpm restart
