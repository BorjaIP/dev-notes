---
id: cx837n42qjbsnwquqsrjor3
title: Ecr
desc: ''
updated: 1655751319850
created: 1655742555092
---

# ECR

- [Using Amazon ECR Images with Amazon ECS](https://docs.aws.amazon.com/AmazonECS/latest/userguide/ecr-repositories.html)

Para registrarse en `ECR` necesitas saber primero saber el password para el login usando este comando:

```bash
aws ecr get-login-password --profile utile | docker login --username AWS --password-stdin 583392431550.dkr.ecr.eu-west-1.amazonaws.com
aws ecr get-login --registry-ids 583392431550 --no-include-email --profile utile
```


