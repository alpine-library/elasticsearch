FROM  anapsix/alpine-java:latest
MAINTAINER Ekozan

RUN addgroup elasticsearch && adduser -S -G elasticsearch elasticsearch

RUN apk -U add ca-certificates curl

ENV ELASTICSEARCH_VERSION 2.0.0

RUN \
  mkdir -p /opt && \
  cd /tmp && \
  curl https://download.elasticsearch.org/elasticsearch/release/org/elasticsearch/distribution/tar/elasticsearch/2.0.0/elasticsearch-$ELASTICSEARCH_VERSION.tar.gz > elasticsearch-$ELASTICSEARCH_VERSION.tar.gz && \
  tar -xzf elasticsearch-$ELASTICSEARCH_VERSION.tar.gz && \
  rm -rf elasticsearch-$ELASTICSEARCH_VERSION.tar.gz && \
  mv elasticsearch-$ELASTICSEARCH_VERSION /opt/elasticsearch && \
  chown -R elasticsearch:elasticsearch /opt/elasticsearch && \
  mkdir -p /var/lib/elasticsearch && \
  chown -R elasticsearch:elasticsearch /var/lib/elasticsearch


ADD ./elasticsearch.yml /opt/elasticsearch/config/elasticsearch.yml

COPY docker-entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

RUN curl -o /usr/local/bin/gosu -SL "https://github.com/tianon/gosu/releases/download/1.6/gosu-amd64"
RUN chmod +x /usr/local/bin/gosu


VOLUME ["/data"]

EXPOSE 9200
EXPOSE 9300

CMD ["/entrypoint.sh"]
