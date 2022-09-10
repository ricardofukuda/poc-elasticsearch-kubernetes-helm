# POC - ElasticSearch Stack on Kubernetes using Helm
```
helm repo add elastic https://helm.elastic.co
```
## Generate admin credentials and certificates
It's going to automatically generate and apply the secrets into "elk" kubernetes namespace.\

```
kubectl create namespace elk
sh ./elasticsearch/scripts/setup-security.sh
```

## Install ElasticSearch
```
helm upgrade --install elasticsearch-master -n elk --version 7.17.3 -f elasticsearch/values-master.yaml elastic/elasticsearch
helm upgrade --install elasticsearch-data -n elk --version 7.17.3 -f elasticsearch/values-data.yaml elastic/elasticsearch
```
## Install Kibana
```
helm upgrade --install kibana -n elk --version 7.17.3 -f kibana/values.yaml elastic/kibana
```
## Install Filebeat
```
helm upgrade --install filebeat -n elk --version 7.17.3 -f filebeat/values.yaml elastic/filebeat
```
## Install Logstash
```
helm upgrade --install logstash -n elk --version 7.17.3 -f logstash/values.yaml elastic/logstash
```
## Install APM Server
```
helm upgrade --install apm-server -n elk --version 7.17.3 -f apm-server/values.yaml elastic/apm-server
```
## Install Metricbeat
```
helm upgrade --install metricbeat -n elk --version 7.17.3 -f metricbeat/values.yaml elastic/metricbeat
```
