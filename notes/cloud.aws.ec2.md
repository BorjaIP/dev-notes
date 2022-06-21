---
id: 4pzzoh927yvyh23fneoni3g
title: EC2
desc: ''
updated: 1655798972259
created: 1655726069394
---

# EC2

- **EC2** Instance Types based on compute resources [Details](https://cloudacademy.com/blog/aws-ec2-instance-types-explained/).

![](assets/images/ec2-types.jpg)

- **EC2** Instance Types based on prices [Prices](https://aws.amazon.com/ec2/instance-types/?nc1=h_ls).

- [Pricing comparing instances](https://instances.vantage.sh/?region=eu-west-1)

## AWS Savings Plans

EC2 offer clients **with regular usage expectations** the opportunity to lock in significant discounts off On-Demand pricing in return for commiting to **one or three-year** terms of use. If you’re able to pay part or all of this cost up front, AWS will tack on an additional discount.

EC2 Instance [Savings Plans](https://aws.amazon.com/savingsplans/compute-pricing/) offer even steeper **discounts but are less flexible**. First of all, Fargate customers can’t use these plans, and **you’re locked into a specific EC2 Instance family and region for the duration of your term**. However, these discounts can reach as high as **72 percent**, so if you’re sure you’ll use the instances, this is a great option.

### Payment Plans

- With **up front** you pay everithing in up front with saving costs. (The more you pay up front the more you save)
- **Partial** with payment up front, when you pay parcial each period and up front pay.
- Nothing **up front** only parcial. (This is little more expensive)

## Spot Instances

[Spot Instances](https://www.cloudforecast.io/blog/are-aws-spot-instances-worth-it-in-production/) are another way to purchase computing power at a steep discount. AWS allows **customers to purchase unused capacity**, but if the capacity is purchased by another user, **it will be reclaimed with a two-minute warning**. These discounts change slowly based on market demand; currently they are 67 percent for Fargate compute and up to 90 percent for EC2 Instances.

## AWS ECS Container Optimization

### Right Sizing

Container resources are often allocated **once, then never reevaluated**. Load **testing your container** applications can help you minimize the amount of resources a container requests, while ensuring that your application can handle its workload.

### Auto Scaling

To further optimize container usage, particularly with unpredictable workloads, look into **auto scaling the tasks running in your cluster**.

### AWS ECS Container Consolidation

Consolidate smaller or similar services into a **single container**. For example, if you have a container to handle internal traffic and a container to handle external traffic, be aware that ECS supports multiple load balancer target groups.


---

# References

[1]: https://d1.awsstatic.com/whitepapers/docker-on-aws.pdf?contd_dop4 "Docker on AWS"