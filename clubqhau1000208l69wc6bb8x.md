---
title: "Prometheus and Grafana Set up"
datePublished: Thu Mar 28 2024 21:15:21 GMT+0000 (Coordinated Universal Time)
cuid: clubqhau1000208l69wc6bb8x
slug: prometheus-and-grafana-set-up

---

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711653516328/8d46ea37-31da-4f6e-adcf-c4ada60c2e48.png align="center")

```yaml
version: '3'

services:
  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus:/etc/prometheus
    command:
      - "--config.file=/etc/prometheus/prometheus.yml"

  node-exporter:
    image: prom/node-exporter
    ports:
      - "9100:9100"
```

```yaml
global:
  scrape_interval:     15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'node'
    static_configs:
      - targets: ['node-exporter:9100']
```

The above is prometheus.yml

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711654177690/be0c2a6e-c8d1-4ba0-922c-bb5571b25c69.png align="center")

```yaml
services:
  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=Agopq
    volumes:
      - ./grafana:/var/lib/grafana
```

The above is docker-compose for grafana.

you can have entire Monotiring in single docker-compose.yml

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711658013343/e1fd257f-80d1-4685-b131-1df70dd41bfe.png align="center")

```yaml
version: '3'

services:
  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus:/etc/prometheus
    command:
      - "--config.file=/etc/prometheus/prometheus.yml"

  node-exporter:
    image: prom/node-exporter
    ports:
      - "9100:9100"

  grafana:
    image: grafana/grafana
    ports:
      - "3000:3000"
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=Agopq
    volumes:
      - ./grafana:/var/lib/grafana

  alertmanager:
    image: prom/alertmanager
    ports:
      - "9093:9093"
    volumes:
      - ./alertmanager:/etc/alertmanager
    command:
      - "--config.file=/etc/alertmanager/alertmanager.yml"
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1711660402045/bafd3225-3bb5-4fff-93f6-839fcf46fe23.png align="center")