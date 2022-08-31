# AWS Cost Optimization Resources for Startups
Welcome. This reference has been prepared by Startup Solution Architects at AWS to help Startups easily find additional resources that provide specific guidance on various techniques for effective cost optimization.  

We hope this proves useful as you navigate the various options available to you for maximizing the value you can get out of running on AWS. As always, should you have questions on anything, please don't hesitate to contact your local startup team. you can also email ~~<sup-apj@amazon.com>~~

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Contents

- [Useful Tools](#useful-tools)
  - [AWS Budgets](#aws-budgets)
  - [Cost Explorer](#cost-explorer)
  - [Trusted Advisor](#trusted-advisor)
  - [Anomaly detection?](#anomaly-detection)
  - [AWS Organizations](#aws-organizations)
  - [Tagging](#tagging)
- [No Effort Options](#no-effort-options)
  - [Reserved Instances](#reserved-instances)
  - [Savings Plans](#savings-plans)
- [Services](#services)
  - [DynamoDB](#dynamodb)
  - [EBS](#ebs)
  - [EC2](#ec2)
  - [ECS](#ecs)
  - [EKS](#eks)
  - [RDS](#rds)
  - [S3](#s3)
  - [Spot](#spot)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
  
    
<br>
<br>
<br>

# Useful Tools

## AWS Budgets

## Cost Explorer

## Trusted Advisor

## Anomaly detection?

## AWS Organizations

Account setup.  
Control tower?



## Tagging







# No Effort Options


## Reserved Instances

## Savings Plans




# AWS Product and Services

## Data Transfer Out

Avoid the anti pattern of inter service communication going out to the internet and coming back in. Use Gateway endpoints! They are free. 
https://docs.aws.amazon.com/vpc/latest/privatelink/gateway-endpoints.html

For services other than S3 and DynamoDB you need an interface endpoint.
https://docs.aws.amazon.com/vpc/latest/privatelink/aws-services-privatelink-support.html

https://aws.amazon.com/privatelink/pricing/
Min charge is 0.013 * 730 = $9.49
And then $0.01 / PB

Look at this if your DTO for interservice communication is higher than this.

It's important to understand what charges you incur for data transfer. This blog explores data transfer costs in relation to RDS. It's worth noting that aside from removing undifferentiated heavy lifting, using managed services also exempts you from certain data transfer charges within a region.
https://aws.amazon.com/blogs/architecture/exploring-data-transfer-costs-for-aws-managed-databases/



## DynamoDB

## EBS
In general, for almost all workloads, if you are on GP2 you will benefit from moving to GP3.
https://aws.amazon.com/about-aws/whats-new/2020/12/introducing-new-amazon-ebs-general-purpose-volumes-gp3/

Find out how much you stand to save with this EBS GP2 to GP3 Cost savings calculator: https://d1.awsstatic.com/product-marketing/Storage/EBS/gp2_gp3_CostOptimizer.dd5eac2187ef7678f4922fcc3d96982992964ba5.xlsx
  
Here's a blog post describing how you can migrate your Amazon EBS volumes from gp2 to gp3 and save up to 20% on costs: https://aws.amazon.com/blogs/storage/migrate-your-amazon-ebs-volumes-from-gp2-to-gp3-and-save-up-to-20-on-costs/

## EC2

Deploy ready to use Instance Scheduler, allowing you to start and stop instances on a schedule to help save costs.
https://aws.amazon.com/solutions/implementations/instance-scheduler/

Consider alternate processors  (often 10% cheaper)
https://aws.amazon.com/ec2/amd/

ARM based (up to 40% better price over performance.)  
https://aws.amazon.com/ec2/graviton/



## ECS
ECS Fargate is a highly recommended way for startups to deploy their applications as it  removes undifferentiated heavy lifting of managing instances. This blog post is a cost optimization checklist to help you optimize on cost.
https://aws.amazon.com/blogs/containers/cost-optimization-checklist-for-ecs-fargate/


To further optimize you can use Fargate spot, but you need to architect for handling the interruptions if the computer resources get reclaimed.  
This japanese blog post describes how to do that.
https://aws.amazon.com/blogs/containers/graceful-shutdowns-with-ecs/  
[JP version]
https://aws.amazon.com/jp/blogs/news/graceful-shutdowns-with-ecs/


Container insights is super helpful for gaining visiblity into what your containers are doing. This blog introduces the product and what you can do with it
https://aws.amazon.com/blogs/mt/introducing-container-insights-for-amazon-ecs/


For a full list of Amazon ECS Container Insights metrics, see Amazon ECS Container Insights Metrics https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Container-Insights-metrics-ECS.html



## EKS

There are various tools and plugins you should know about to help you optimize your EKS usage.

AWS Node Terimination handler helps you gracefully handle EC2 instance shutdown within Kubernetes. https://github.com/aws/aws-node-termination-handler
This is important for auto scaling and leveraging spot.

[Karpenter](https://karpenter.sh/) is a high performance auto scaling solution. Use it with Spot to reap savings. https://aws.amazon.com/blogs/containers/using-amazon-ec2-spot-instances-with-karpenter/

This blog post describes recommended tips for cost optimization in AWS.
https://aws.amazon.com/blogs/containers/cost-optimization-for-kubernetes-on-aws/

These plugins will help give visibility into your costs
https://github.com/hjacobs/kube-resource-report  



another helpful tool for cost visibility is [Kubecost](https://github.com/kubecost/kubectl-cost). Kubecost enables users to view costs broken down by Kubernetes resources including pods, nodes, namespaces, labels, and more. 
https://aws.amazon.com/blogs/containers/aws-and-kubecost-collaborate-to-deliver-cost-monitoring-for-eks-customers/

use it in conjunction with 
https://github.com/kubecost/cost-model  


AWS also has cluster level cost allocation tagging.
https://aws.amazon.com/about-aws/whats-new/2022/08/amazon-eks-cluster-level-cost-allocation-tagging/  

[JP version]
https://aws.amazon.com/jp/about-aws/whats-new/2022/08/amazon-eks-cluster-level-cost-allocation-tagging/


This plugin is used to scale in and out the deployments based on time of day. This can result in significant cost-savings when there are many deployments that only need to be available during business hours.
https://github.com/hjacobs/kube-downscaler




## Graviton

github graviton link


## RDS

Understanding how you are using your RDS instances is key to RDS optimization. A highly effective tool to aid you in this is `Performance Insights`  
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PerfInsights.html


These links provide practical hands on workshops to show you how to leverage Performance Insights to get the most out of your RDS instances

Performance Monitoring Workshop for RDS PostgreSQL and Aurora PostgreSQL - https://catalog.us-east-1.prod.workshops.aws/workshops/31babd91-aa9a-4415-8ebf-ce0a6556a216/en-US


RDS MySQL Performance Insights Lab - https://catalog.us-east-1.prod.workshops.aws/workshops/0135d1da-9f07-470c-9845-44ead3c78212/en-US/lab8

This workshop is part of a new program we run with startups to help developers be better practioners of relational databases. If you are interested in running this for your startup, please get in touch with us.  
DB4Dev workshop - https://catalog.workshops.aws/db4devs/en-US



## S3

This workshop walks you through S3 Cost optimization tips: https://catalog.us-east-1.prod.workshops.aws/workshops/f238037c-8f0b-446e-9c15-ebcc4908901a/en-US/002-services/002-storage/003-s3


This blog post will outline how you can optimize for both predictable and dynamic access patterns - https://aws.amazon.com/blogs/storage/amazon-s3-cost-optimization-for-predictable-and-dynamic-access-patterns/


## Spot
AWS Spot Instances are an amazing option allowing you to take advantage of spare capacity in AWS datacenters to receive up to 90% discounts on your instances. Spot is available to use with EC2 instances directly and also with ECS and EKS. You can learn more here 
[https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-spot-instances.html)

The catch is if AWS needs that spare capacity, you will receive a 2 min warning before your instance is reclaimed. 

To learn how you might take advantage of this, you can try yourself in this workshop:
https://ec2spotworkshops.com/


# Other Resources

Workshops and documentation on various topics.
https://trailblazing.report/costoptimization.html
