FROM jenkins/jenkins:lts-alpine
MAINTAINER Pavlov <ppavlov@dontmail.me>

LABEL name="jenkins-master"
LABEL version="2.107"
LABEL maintainer "ppavlov@dontmail.me"
LABEL architecture="x86_64"

# Whether to skip setup wizard
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

# Creates username and password specified through environment variables JENKINS_USER_SECRET and JENKINS_PASS_SECRET
COPY security.groovy /usr/share/jenkins/ref/init.groovy.d/security.groovy
COPY executors.groovy /usr/share/jenkins/ref/init.groovy.d/executors.groovy

# Install a list of plugins from the file 'plugins.txt' and their dependencies
COPY plugins.txt /usr/share/jenkins/ref/
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/ref/plugins.txt
