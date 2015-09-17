FROM debian:wheezy

RUN apt-get update && apt-get -y install libfontconfig wget adduser openssl ca-certificates && apt-get clean

RUN wget http://grafanarel.s3.amazonaws.com/builds/grafana_latest_amd64.deb

RUN dpkg -i grafana_latest_amd64.deb

WORKDIR /tmp

RUN wget https://github.com/grafana/grafana-plugins/archive/master.zip
RUN apt-get install unzip
RUN unzip master.zip
RUN cp -R grafana-plugins-master/datasources/* /usr/share/grafana/public/app/plugins/datasource/


EXPOSE 3000

VOLUME ["/var/lib/grafana"]
VOLUME ["/var/log/grafana"]
VOLUME ["/etc/grafana"]

WORKDIR /usr/share/grafana

ENTRYPOINT ["/usr/sbin/grafana-server", "--config=/etc/grafana/grafana.ini", "cfg:default.paths.data=/var/lib/grafana", "cfg:default.paths.logs=/var/log/grafana"]
