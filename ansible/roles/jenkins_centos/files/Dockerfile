FROM jenkins/jenkins:latest
USER root
RUN apt-get update && apt-get install -y --no-install-recommends \
       apt-transport-https \
       ca-certificates curl gnupg2 \
       software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/debian \
       $(lsb_release -cs) stable"
RUN apt-get update && apt-get install -y docker-ce-cli

# ENV JAVA_OPTS -Djenkins.install.runSetupWizard=false
# ENV CASC_JENKINS_CONFIG /var/jenkins_home/casc.yaml
COPY --chown=jenkins:jenkins plugins.txt /usr/share/jenkins/ref/plugins.txt

#USER jenkins
RUN jenkins-plugin-cli -f /usr/share/jenkins/ref/plugins.txt

COPY --chown=jenkins:jenkins casc.yaml /var/jenkins_home/casc.yaml
