FROM alaneduardo/base
MAINTAINER Alan Eduardo <alan_eduardo@outlook.com.br>

ENV DB_PASSWORD docker
ENV ROLE pgsql

EXPOSE 5432

RUN sed -i.bak '/^\[base\]/a exclude=postgresql\*' /etc/yum.repos.d/CentOS-Base.repo
RUN sed -i.bak '/^\[updates\]/a exclude=postgresql\*' /etc/yum.repos.d/CentOS-Base.repo
RUN rpm -Uvh http://yum.postgresql.org/9.3/redhat/rhel-6-x86_64/pgdg-centos93-9.3-1.noarch.rpm
RUN yum install -y postgresql93-server postgresql93-devel postgresql93-contrib

RUN service postgresql-9.3 initdb

ADD pg_hba.conf /var/lib/pgsql/9.3/data/pg_hba.conf
ADD pg_ident.conf /var/lib/pgsql/9.3/data/pg_ident.conf
ADD postgresql.conf /var/lib/pgsql/9.3/data/postgresql.conf
ADD program-postgresql.conf /etc/supervisor.d/

RUN touch /etc/sysconfig/network

RUN echo 'HOSTNAME=db.postgresql' >> /etc/sysconfig/network

VOLUME ["/var/lib/pgsql/9.3/data"]