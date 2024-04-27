---
title: "Elasticsearch and Kibana Installation"
seoTitle: "Elastic search and Kibana"
seoDescription: "Elasticsearch: A powerful search and analytics engine that can index and search large volumes of data quickly. It uses a distributed architecture to manage "
datePublished: Sat Apr 27 2024 05:28:00 GMT+0000 (Coordinated Universal Time)
cuid: clvhnuk6i000109ld58clg7mk
slug: elasticsearch-and-kibana-installation
tags: monitoring, devops, elk-stack, elk-installation

---

Setting up elasticsearch as per offical document

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714107363768/ede4c8e6-be99-490d-a614-f7ae2defe185.png align="center")

Make sure you have opened 9200, 9300 port opened.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714107498136/657735ab-b759-437b-a51c-ba3e5177a161.png align="center")

Now start the service using systemd and note down password or else you can reset if needed.

Now Install kibana

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714107740692/98dfa580-53fb-402a-832b-4b2f7bb8c16a.png align="center")

Start the service using systemd and make sure you have opened 5601 port, under /etc/kibana/kibana.yml make sure [server.host](http://server.host): is set to "0.0.0.0" to access kibana apart from localhost, so you can acess from your browser.

Run the following code, it generates a token that you need to enter while accessing kibana in browser and then it asks for verification code you will have it when you started kibana using systemd service if not check status using systemd the outpt will have verification code.

```bash
/usr/share/elasticsearch/bin/elasticsearch-create-enrollment-token -s kibana
```

next is asks for elastic username and password, elastic is username and you will have you pasword will installing it or also you can reset it.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1714108392704/d668983a-c198-4913-b492-e9f6820cff30.png align="center")

This is same even when you install through archive but we have now done using debian package.

[Elasticsearch Installation link](https://www.elastic.co/guide/en/elasticsearch/reference/current/install-elasticsearch.html)

[Kibana Installation link](https://www.elastic.co/guide/en/kibana/current/install.html)