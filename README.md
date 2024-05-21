# Equinor Cloud Infrastructure Monitoring Guide

## For å sette opp Artifactory

Enter sudo   
```
sudo su
```

Lage mappe
```
mkdir /opt/jmx
cd /opt/jmx
```
Laste ned exporteren
```
wget https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.20.0/jmx_prometheus_javaagent-0.20.0.jar
```

Lage en basic config
```
printf 'rules:\n- pattern: ".*"\n' | sudo tee config.yaml > /dev/null
```


Installere Fluentd
```
curl -fsSL https://toolbelt.treasuredata.com/sh/install-redhat-fluent-package5-lts.sh | sh
```
 
Installere Prometheus Fluentd-plugin
```
fluent-gem install fluent-plugin-prometheus fluent-plugin-grafana-loki fluent-plugin-loki
```

Gå til etc/fluent mappen og kopier innholdet fra artifactory/fluentd.conf til /etc/fluent/fluent.conf
```
cd /etc/fluent
nano fluentd
```
Kopier artifactory/fluentd.service til /etc/systemd/system/fluent.service
```
cd /etc/systemd/system/
nano fluent.service
```

Gjør log filene til Artifactory readable
```
chmod a+r -R /opt/jfrog/artifactory/var/log
```
Kjør fluentd 
```
systemctl start fluentd 
```

