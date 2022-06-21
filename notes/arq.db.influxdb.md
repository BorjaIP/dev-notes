---
id: dr4nt7pqwkco6ifadnv6gyb
title: InfluxDB
desc: ''
updated: 1655801225508
created: 1655800094976
---

# InfluxDB

## Types

- InfluxDB Cloud: Data platform on the Cloud in [AWS](https://www.influxdata.com/partners/aws/) or other Cloud Provider. You need pay a **subscription service** and only in Europe (Frankfurt).
- InfluDB Enterprise: A subscription for install on Cloud or on-premise.
- InfluxDB OSS: Open Source solution for on premise. No HA or clustering

[Choose the version that best matches your needs](https://www.influxdata.com/products/editions/)

## Architecture for HA/Clustering

- **Meta nodes**: Meta nodes hold all of the following meta data:

    - all nodes in the cluster and their role
    - all databases and retention policies that exist in the cluster
    - all shards and shard groups, and on what nodes they exist
    - cluster users and their permissions
    - all continuous queries

- **Data nodes**: Data nodes hold all of the raw time series data and metadata, including:

    - measurements
    - tag keys and values
    - field keys and values

