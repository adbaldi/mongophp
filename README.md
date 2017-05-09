# mongophp

Dockerfile used to create builder image
----------------------------------------------
```
# php-devel-70-centos7
FROM centos/php-70-centos7

# Put the maintainer name in the image metadata
MAINTAINER CSPS Team

# Set labels used in OpenShift to describe the builder image
LABEL io.k8s.description="Platform for building PHP applications with additional modules" \
      io.k8s.display-name="Apache 2.4 with PHP 7.0 development packages" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="builder,php,php-devel"

# Temporarily set the user to root
USER root

# Install required packages 
RUN yum install -y --setopt=tsflags=nodocs rh-php70-php-devel libaio && yum clean all -y 

# This default user is created in the openshift/base-centos7 image
USER 1001

# Set the default port for applications built using this image
EXPOSE 8080

# Set the default CMD for the image
CMD ["usage"]
```
