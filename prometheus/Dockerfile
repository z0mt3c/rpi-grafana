FROM resin/rpi-raspbian:jessie

ENV PROMETHEUS_VERSION 1.4.1

RUN apt-get update && apt-get install wget
RUN wget -q https://github.com/prometheus/prometheus/releases/download/v${PROMETHEUS_VERSION}/prometheus-${PROMETHEUS_VERSION}.linux-armv7.tar.gz && \
    mkdir -p /opt/prometheus && \
    tar xvfz prometheus-${PROMETHEUS_VERSION}.linux-armv7.tar.gz --strip-components=1 -C /opt/prometheus && \
    rm prometheus-${PROMETHEUS_VERSION}.linux-armv7.tar.gz

WORKDIR /opt/prometheus

RUN mkdir -p /usr/share/prometheus && \
  mkdir -p /etc/prometheus && \
  mv ./prometheus.yml /etc/prometheus/ && \
  mv ./prometheus /usr/bin/ && \
  mv ./promtool /usr/bin/ && \
  mv ./console_libraries /usr/share/prometheus/ && \
  mv ./consoles /usr/share/prometheus/ && \
  ln -s /usr/share/prometheus/console_libraries /etc/prometheus/

EXPOSE 9090
VOLUME [ "/prometheus" ]
WORKDIR /prometheus
ENTRYPOINT [ "/usr/bin/prometheus" ]
CMD ["-config.file=/etc/prometheus/prometheus.yml", \
     "-storage.local.path=/prometheus", \
     "-web.console.libraries=/usr/share/prometheus/console_libraries", \
     "-web.console.templates=/usr/share/prometheus/consoles" ]
