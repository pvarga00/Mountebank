
## Overview

This document will go over the process of getting Mountebank up and running in AWS, for your Release Train.

## What You'll Need

Before starting, you will need the following information:

1. AWS Account
    1. Account ID
    2. VPC
    3. Subnets (private subnets for the ECS Cluster and public subnets for the ALB)
    4. Hosted zone with the desired DNS domain name
2. An AWS Access and Secret Key that has permissions to push docker images to ECR
3. [The mountebank-starter-kit repository](https://git.rockfin.com/terraform-emerging/mountebank-starter-kit) -- which you have either forked or created a new repo and placed the contents of the starter kit into.




## Table Of Contents:

- <ac:link><ri:page ri:content-title="1 - Configuring Infrastructure"></ri:page></ac:link>
- <ac:link><ri:page ri:content-title="2 - Deploying Infrastructure With HAL"></ri:page></ac:link>
- <ac:link><ri:page ri:content-title="3 - Configuring Application Deployment"></ri:page></ac:link>
- <ac:link><ri:page ri:content-title="4 - Updating CircleCI and HAL .YAML Files"></ri:page></ac:link>
- <ac:link><ri:page ri:content-title="5 - Building And Deploying"></ri:page></ac:link>



