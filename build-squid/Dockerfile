FROM arm64v8/ubuntu:20.04                                    

ENV TERM=xterm

# send over selections
COPY files/deb-selections /deb-selections
RUN debconf-set-selections /deb-selections

# perform packages install
COPY files/packages /packages                                                       
RUN apt-get update && \
    xargs -t -a /packages apt-get install -y && \
    apt-get clean

# send over sudoers file for proxy user
COPY files/proxy /etc/sudoers.d/proxy

# send over config
COPY conf.d /etc/squid/conf.d

EXPOSE 3128/tcp

USER proxy
ENTRYPOINT ["/usr/bin/sudo", "/usr/sbin/squid", "--foreground"]
