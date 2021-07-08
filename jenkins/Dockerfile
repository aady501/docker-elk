FROM jenkins/jenkins:latest
USER root
RUN apt-get update && apt-get install -y apt-transport-https \
       ca-certificates curl gnupg2 \
       software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/debian \
       $(lsb_release -cs) stable"
RUN apt-get update && apt-get install -y docker-ce-cli
RUN curl -o /tmp/filebeat_1.0.1_amd64.deb https://download.elastic.co/beats/filebeat/filebeat_1.0.1_amd64.deb && \
    dpkg -i /tmp/filebeat_1.0.1_amd64.deb &&  apt-get install
COPY filebeat.yml /etc/filebeat/filebeat.yml

# RUN /etc/init.d/filebeat start
# USER jenkins
# RUN jenkins-plugin-cli --plugins "blueocean:1.24.7 docker-workflow:1.26"

COPY ["entrypoint.sh", "/"]
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/bin/bash","-c","./entrypoint.sh"]

