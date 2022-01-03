FROM ubuntu:16.04 

RUN apt-get update 

# installs ping, netstat for debugging purposes
# installing tzdata will fix NESSUS_TZ_DIR related warning
RUN apt-get install -y net-tools iputils-ping tzdata

RUN rm -rf /var/lib/apt/lists/*

#Place you Nessus-<latest-version>-ubuntu1110_amd64.deb in the same folder
COPY Nessus-10.0.2-ubuntu1110_amd64.deb /tmp/Nessus.deb

RUN dpkg -i /tmp/Nessus.deb

# defaut Nessus Scanner port
EXPOSE 8834

ENTRYPOINT [ "/opt/nessus/sbin/nessusd" ]
# ENTRYPOINT [ "/etc/init.d/nessusd start" ]
