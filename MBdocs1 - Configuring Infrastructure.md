
## Overview

In this section, we will go over the process of updating the starter kit to use your AWS account, along with an initial HAL application setup.
<ac:structured-macro ac:name="info" ac:schema-version="1" ac:macro-id="79a3f20a-bdc3-422d-b028-2c89101baa7b"><ac:rich-text-body><p>This is&nbsp;<strong>part 1</strong>&nbsp;of a series of configuring your instance of Mountebank. <ac:link><ri:page ri:content-title="Mountebank: Getting Mountebank Up And Running in AWS"></ri:page><ac:plain-text-link-body><![CDATA[Please reference the entrypoint to follow the guide]]></ac:plain-text-link-body></ac:link></p></ac:rich-text-body></ac:structured-macro>


## What You'll Need

Before starting, you will need the following information

1. AWS Account
    1. Account ID
    2. VPC
    3. Subnets (private subnets for the ECS Cluster and public subnets for the ALB)
    4. Hosted zone with the desired DNS domain name
2. [The mountebank-starter-kit repository](https://git.rockfin.com/krobertson1/mountebank-starter-kit) , which you have either forked or created a new repo and placed the contents of the starter kit into.




## Configuring HAL Application

You will need to make an Application in HAL in order to push this infrastructure. Below are steps on configuring this.

1. From the **Apps** page on HAL, click on **Add Application**
2. Fill out the following fields
    1. **Name -**you can use a format like **{ApplicationName}ServiceMocking-IAC.**e.g.: RocketMortgageServiceMocking-IAC
    2. **Organization -** An Organization in HAL containers the credentials for your AWS account(s), so select the organization that has the accounts tied to it you wish to push to. e.g.: Client Driven Experiences
    3. **GitHub Enterprise Repository** - Enter either your forked starter kit URL or if you made a custom repository, use that URL. e.g.: [https://git.rockfin.com/RocketMortgage/ServiceMocking.git](https://git.rockfin.com/RocketMortgage/ServiceMocking.git)
    4. **Provider** - Select **AWS**
    5. **Platform** - Select **Infrastructure As Code**
    6. **Language** - Select **Terraform**
3. Click on**Show advanced options**and set**Multi-solution project**to **/Infrastructure

<ac:image ac:height="400"><ri:attachment ri:filename="image2019-1-28_10-7-26.png"></ri:attachment></ac:image>**
4. Open the application and make note of the **application ID** in the HAL URL

<ac:image ac:height="173"><ri:attachment ri:filename="image2019-1-28_10-19-12.png"></ri:attachment></ac:image>


## Updating the Infrastructure Folder Structure

When looking at the Infrastructure folder of the starter kit, you will see the following structure:
<ac:structured-macro ac:name="code" ac:schema-version="1" ac:macro-id="66953f3b-3656-427d-b045-af7d37918ed8"><ac:parameter ac:name="language">bash</ac:parameter><ac:plain-text-body><![CDATA[Infrastructure--->123456789 #account number	--->us-east-2 #region		-->test #environment			-->ecs-app #module]]></ac:plain-text-body></ac:structured-macro>
To get started quickly, you'll just need to update the **account number** folder name to match the AWS account number you wish to deploy. You can get this from **[awsconsole/](https://confluence/awsconsole/)**

<ac:image ac:height="91"><ri:attachment ri:filename="image2019-1-28_8-57-41.png"></ri:attachment></ac:image>

If you wish to further customize your infrastructure (for example, change the region or "environment", you can update the names of the **region** and **environment** folder to your liking.

## Updating Infrastructure Files

Within each folder, there will be a different **.tfvars** file. If you just updated the account number folder, then you'll just need to update the following:

1. Update the **account.tfvars** folder to set your aws\_account\_id

<ac:image ac:height="250"><ri:attachment ri:filename="image2019-1-28_9-13-31.png"></ri:attachment></ac:image>

<ac:structured-macro ac:name="info" ac:schema-version="1" ac:macro-id="6d182d61-025e-4700-859d-eedefbd1d0af"><ac:rich-text-body><p>If you also updated the region or environment folder, you will need to update the <strong>region.tfvars</strong> and <strong>env.tfvars</strong> , respectively.</p></ac:rich-text-body></ac:structured-macro>


You will also need to update the **terraform.tfvars** file within the **ecs-app** folder. There are quite a few variables to replace here. They are listed below:

1. **aws\_region** - Change AWS region to **your region folder name**
2. **app\_tags**
    1. **development-team-email** - Update to your primary engineering team's distribution
    2. **infrastructure-team-email** - Update to the infrastructure team's distribution
    3. **infrastructure-engineer-email** - Update to infrastructure owner's email address.
    4. **hal-app-id** - Application ID in HAL of HAL App to push infrastructure (the one from above)
3. **vpc\_id** - ID of the VPC you wish to place the infrastructure in
4. **subnet\_ids** - Subnet Ids of the **private** subnets this infrastructure should be in
5. **alb\_public\_subnet\_ids** - Subnet Ids of the **public** (or QL public) subnets that will be associated with the **ALB** (Application Load Balancer)
6. **route\_53\_zone\_id** - The ID of the Hosted Zone in Route53 you wish to use.
7. **website\_dns\_name** - The DNS name you wish to use to communicate with Mountebank. The format will be **{nameofyourchoice}.{yourhostedzonedomain}**. e.g. **[testmock.np.rocketmortgage.com](http://testmock.np.rocketmortgage.com/ "http://testmock.np.rocketmortgage.com/")**
8. **application\_name** - "Application" Name you wish to associate with infrastructure. eg: **RocketMortgage-mb**
9. **environment** - Environment this infrastructure lives in. **Recommended**: Make the the name of the environment folder.


Once these changes are made, check them in.


