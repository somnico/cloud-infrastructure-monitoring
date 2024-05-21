# Equinor Cloud Infrastructure Monitoring Guide
Enter sudo   
```sudo su```

Lage mappe
```
mkdir /opt/jmx
cd /opt/jmx
```
Laste ned exporteren
```wget https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.20.0/jmx_prometheus_javaagent-0.20.0.jar```

# Lage en basic config
printf 'rules:\n- pattern: ".*"\n' | sudo tee config.yaml > /dev/null




# For oppsett av Fluentd 

# Enter sudo
sudo su

# Installere Fluentd
curl -fsSL https://toolbelt.treasuredata.com/sh/install-redhat-fluent-package5-lts.sh | sh

# Installere Prometheus Fluentd-plugin
fluent-gem install fluent-plugin-prometheus fluent-plugin-grafana-loki fluent-plugin-loki

# Flytt til fluent-mappen og kopier innholdet fra "fluentd.conf.KOPIER" filen til /etc/fluent/fluentd.conf
cd /etc/fluent

# Kopiere fluentd.conf dit

# Gjør log filene readable
chmod a+r -R /opt/jfrog/artifactory/var/log

# Kjør fluentd (må være i /etc/fluentd dir)
fluentd -c fluentd.conf &

# For å stoppe: ctrl + z

# For å fjerne prosessen
pkill -9 -f fluentd
