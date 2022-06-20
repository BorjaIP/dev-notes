---
id: eg76udplsw4zwbba6dd4tag
title: Aws
desc: ''
updated: 1655726061351
created: 1655319754248
---

## Configuration

```bash
# configure aws for specific user
aws configure --profile profile-name
# user connected
aws --profile name sts get-caller-identity

# EC2 
aws --profile name ec2 describe-instances --query "Reservations[].Instances[].[Tags[?Key=='Name'],InstanceId,State.Name]" --output text
aws --profile name ec2 start-instances --instance-ids ID
aws --profile name ec2 stop-instances --instance-ids ID
aws --profile sbri ec2 describe-instances --query "Reservations[].Instances[].[PublicIpAddress]" --output text
# RDS start & stop
aws --profile name rds stop-db-instance --db-instance-identifier name
aws --profile name rds start-db-instance --db-instance-identifier name
```

- [[ECS | cloud.aws.ecs]]

# ECR

Para registrarse en `ECR` necesitas saber primero saber el password para el login usando este comando:

```bash
aws ecr get-login-password --profile utile | docker login --username AWS --password-stdin 583392431550.dkr.ecr.eu-west-1.amazonaws.com
aws ecr get-login --registry-ids 583392431550 --no-include-email --profile utile
```


# EKS
aws eks --region eu-west-1 update-kubeconfig --profile utile
