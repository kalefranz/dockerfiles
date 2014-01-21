#################################################################
# Creates a logstash container
#
#                    ##        .
#              ## ## ##       ==
#           ## ## ## ##      ===
#       /""""""""""""""""\___/ ===
#  ~~~ {~~ ~~~~ ~~~ ~~~~ ~~ ~ /  ===- ~~~
#       \______ o          __/
#         \    \        __/
#          \____\______/
#
# Author:    Kale Franz <kale@franz.io>
# License:   MIT
#################################################################

FROM kalefranz/centos-java:latest
MAINTAINER Kale Franz <kale@franz.io>


RUN /usr/bin/curl -s 'http://logstash.net/' | gawk 'match($0, /href="https:\/\/download.elasticsearch.org\/([-.a-zA-Z0-9\/]*).jar">Download<\/a>/, ary) {print ary[1]}' | { read LOGSTASH_URL_PART; /usr/bin/wget -O logstash.jar https://download.elasticsearch.org/${LOGSTASH_URL_PART}.jar; }


# a few examples
# https://github.com/dasch/docker-logstash/blob/master/Dockerfile

ADD logstash.conf logstash.conf


EXPOSE 9200
EXPOSE 9300
EXPOSE 9301
EXPOSE 9302
EXPOSE 9292

# Expose the Syslog UDP port.
EXPOSE 514/udp

ENTRYPOINT ["/usr/lib/jvm/java-7-oracle/bin/java", "-jar", "logstash-1.2.2-flatjar.jar", "agent", "-v", "-f", "logstash.conf", "--", "web"]