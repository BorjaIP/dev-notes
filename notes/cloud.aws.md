---
id: eg76udplsw4zwbba6dd4tag
title: Aws
desc: ''
updated: 1655752542101
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
## 

- [[ECS | cloud.aws.ecs]]
- [[ECR | cloud.aws.ecr]]

## Core services for Web App

<u>Static Content</u>

Amazon S3 --> For store static content files.
Amazon Cloudfront --> Chaching for access the application frontstored in S3

<u>Domain management</u>

Amazon Route 53 --> DNS Services, API Routes, Register domain.

<u>API Hosting</u>

Amazon API Gateway + AWS Lambda --> Register a function and upload Lambda and redirect to GW
Aplication Load Balancer + Amazon EC2 --> Deploy inside EC2 a redirecto to LB
Aplicacion Load Balancer + Amazon ECS --> Deploy with Docker images

<u>Database</u>

Amazon RDS --> Typicall SQL servers
Amazon Redshift (BI) --> Very heavy querys and analytics, for huge data and join columns.
Amazon DynamoDB --> NoSQL database (key,value)
Amazon ElasticCache --> Redis, Memcache for store database
Amazon Neptune --> Graph database

<u>Application Orchestration/Coordination</u>

Amazon SNS --> Connect one service to others with some restrictions or rules
Amazon SQS --> Connect one service to others with some restrictions or rules
AWS Step Functions --> Workflow processing or sequence

<u>Analytics, Big Data, ML</u>

Amazon Athnena --> Querys over S3 for analytics
Amazon Quick Sight -> Tableau or PowerBI, build dashboards(BI Tool)
Amazon EMR --> Map Reduce jobs
Amazon Sagemaker --> Build ML with Notebooks

<u>Security</u>

Amazon VPC --> Build digital Firewall around AWS resources, how to access to our applications, ports
AWS IAM --> Configure access for specific resources

<u>Monitoring</u>

Amazon CloudWatch --> Log applications, monitoring, alarms
AWS Cloudtrail --> When you have many users and need track them 

# EKS
aws eks --region eu-west-1 update-kubeconfig --profile utile
