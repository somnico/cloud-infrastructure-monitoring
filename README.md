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

Oppdater innholdet fra artifactory/system.yaml til /opt/jfrog/artifactory/var/etc/system.yaml
```
nano /opt/jfrog/artifactory/var/etc/system.yaml
```

Installere Fluentd
```
curl -fsSL https://toolbelt.treasuredata.com/sh/install-redhat-fluent-package5-lts.sh | sh
```
 
Installere Prometheus Fluentd-plugin
```
fluent-gem install fluent-plugin-prometheus fluent-plugin-grafana-loki fluent-plugin-loki
```

Kopier innholdet fra artifactory/fluentd.conf til /etc/fluent/fluent.conf
```
nano /etc/fluent/fluentd
```

Kopier innholdet fra artifactory/fluentd.service til /etc/systemd/system/fluent.service
```
nano /etc/systemd/system/fluent.service
```

Gjør log filene til Artifactory readable
```
chmod a+r -R /opt/jfrog/artifactory/var/log
```

Kjør fluentd 
```
systemctl start fluentd 
```

## For å sette opp NGINX i prod

Enter sudo
```
sudo su
```

Kopier innholdet fra nginx/nginx.conf til /etc/nginx/nginx.conf
```
nano /etc/nginx/nginx.conf
```

Kopier innholdet fra nginx/status.conf til /etc/nginx/conf.d/status.conf
```
nano /etc/nginx/conf.d/status.conf
```

Kopier innholdet fra nginx/reverse_proxy.conf til /etc/nginx/conf.d/reverse_proxy.conf
```
nano /etc/nginx/conf.d/reverse_proxy.conf
```

Installere Fluentd
```
curl -fsSL https://toolbelt.treasuredata.com/sh/install-redhat-fluent-package5-lts.sh | sh
```
 
Installere Prometheus Fluentd-plugin
```
fluent-gem install fluent-plugin-prometheus fluent-plugin-grafana-loki fluent-plugin-loki
```

Gå til etc/fluent mappen og kopier innholdet fra nginx/fluentd.conf til /etc/fluent/fluent.conf
```
nano /etc/fluentfluentd
```

Kopier innholdet fra nginx/fluentd.service til /etc/systemd/system/fluent.service
```
nano /etc/systemd/system/fluent.service
```


