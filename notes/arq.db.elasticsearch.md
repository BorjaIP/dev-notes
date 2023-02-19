---
id: 3i5fhav92iioxiafg39jvnz
title: Elasticsearch
desc: ''
updated: 1676576710294
created: 1675089115020
---

## Alternatives

Elasticsearch modify her License here is an alternative, [OpenSearch](https://github.com/opensearch-project/OpenSearch).

## Options

Edit `/usr/share/elasticsearch/config/elasticsearch.yml`.

```yaml
cluster.name: "simple"
network.host: 0.0.0.0
xpack.security.enabled: true
discovery.type: single-node
```

```bash
# auto password
./bin/elasticsearch-setup-passwords auto
# setup custom pass
./bin/elasticsearch-setup-passwords interactive
```

## API

`pip install elasticsearch`

```python
from elasticsearch import Elasticsearch
client = Elasticsearch(hosts="http://username:password@es-endpoint:es-port/")
client.info()
```