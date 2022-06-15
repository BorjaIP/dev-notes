---
id: eg76udplsw4zwbba6dd4tag
title: Aws
desc: ''
updated: 1655319781489
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

## ECS

- Image
- Task Definition
  
  Necesitas definir un Task Definition (JSON file) para describir uno o más Containers (hasta 10) para definir todos los parámetros, CPU, Docker image y demás.

- Cluster
  
  El componente principal es el cluster siendo un grupo de EC2 para tener HA. Cada instancia tiene que tener un Container Agent que es el encargado de Attach la intancia al Cluster. ECS optimcize AIM que vienen con todo lo necesario para ejecutarlo Docker dentro.

- Service
  
  Te permite ejecutar un numero de task dentro del cluster.

- Capacity provider
  
  Para el Auto Scaling Group para tener cuantas EC2 intances puedo tener en el cluster.

- [Network Mode](https://docs.aws.amazon.com/AmazonECS/latest/developerguide/task-networking.html) 
- Logging driver

Hay que desplegarlo detrás de un LB.

[Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html)


 export TF_VAR_rds_password=foobarbaz
terraform graph | dot -Tpng > infrastructure_graph.png

psql -U sbri -h sbri-db.cariaknc5efm.eu-west-2.rds.amazonaws.com -p 5432 sbri

terraform destroy -target=aws_ecs_service.sbri-backend -target=aws_ecs_task_definition.sbri-backend -target=module.vpc.aws_eip.nat -target=aws_lb.sbri-lb -target=aws_autoscaling_group.ecs-cluster

# ECR

Para registrarse en `ECR` necesitas saber primero saber el password para el login usando este comando:

```bash
aws ecr get-login-password --profile utile | docker login --username AWS --password-stdin 583392431550.dkr.ecr.eu-west-1.amazonaws.com
aws ecr get-login --registry-ids 583392431550 --no-include-email --profile utile
```


# EKS
aws eks --region eu-west-1 update-kubeconfig --profile utile
