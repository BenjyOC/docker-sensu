FROM debian:jessie

RUN apt-get update && \
    apt-get install -y wget apt-transport-https && \
    apt-get clean

RUN wget -q https://sensu.global.ssl.fastly.net/apt/pubkey.gpg -O- | apt-key add - && \
    echo "deb     https://sensu.global.ssl.fastly.net/apt jessie main" | tee /etc/apt/sources.list.d/sensu.list && \
    apt-get update && \
    apt-get install -y sensu && \
    apt-get clean

COPY conf.d /etc/sensu/conf.d
ADD start /bin/
RUN chmod +x /bin/start

### CLEANUP
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 4567

ENTRYPOINT ["/bin/start"]
