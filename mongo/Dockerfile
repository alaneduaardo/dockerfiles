FROM alaneduardo/base

ENV ROLE mongo
EXPOSE 27017
MAINTAINER Alan Eduardo <alan_eduardo@outlook.com.br>

# Update the repository sources list
ADD mongodb.repo /etc/yum.repos.d/mongodb.repo
RUN yum -y update

################## BEGIN INSTALLATION ######################
# Install MongoDB Following the Instructions at MongoDB Docs
# Ref: http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

# Add the package verification key
RUN yum install -y mongodb-org

# Configure mongod server
RUN service mongod start
ADD mongod.conf /etc/mongod.conf