---
id: jdv6y5ldlaggs34b1cbuf0b
title: Azure
desc: ''
updated: 1655319800603
created: 1655319794558
---

[ACIs](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/container-instances/container-instances-reference-yaml.md)

[Multi container](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/container-instances/container-instances-multi-container-yaml.md)

az login

## Create container

```bash
az container create --resource-group <rg-name> --name <name> --image <image-name> --cpu 1 --memory 1 --registry-login-server <login-server> --registry-username <username> --registry-password <pass> --ports 80
```

### Create container from YAML

```bash
az container create -g <name> --file <file>.yaml
```

### Shor all containers

```bash
az container list -o table
```

### Show resources

```bash
az resource list -g ResourceGroup -o table
az resource list -g ResourceGroup -o yaml
```

## Show container status

```bash
az container show -g ResourceGroup -n name -o table
az container show -g ResourceGroup -n name --query "{Status:instanceView.state}" --out table
```

### Show container logs

```bash
az container logs -g ResourceGroup -n name
```

### Export template

```bash
az container export -g ResourceGroup -n name -f output.yaml
```

### Cost + Billing

Cost Management + Billing > Cost Analysis

Add Filters:

- Group by: service name
- Granilarity: Daily
- Column

