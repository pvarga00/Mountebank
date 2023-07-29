
## Overview

In this section, we will go over the process of configuring a HAL Application to deploy the Mountebank code
<ac:structured-macro ac:name="info" ac:schema-version="1" ac:macro-id="79a3f20a-bdc3-422d-b028-2c89101baa7b"><ac:rich-text-body><p>This is&nbsp;<strong>part 3</strong>&nbsp;of a series of configuring your instance of Mountebank. <ac:link><ri:page ri:content-title="Mountebank: Getting Mountebank Up And Running in AWS"></ri:page><ac:plain-text-link-body><![CDATA[Please reference the entrypoint to follow the guide]]></ac:plain-text-link-body></ac:link></p></ac:rich-text-body></ac:structured-macro>
## Configuring HAL Application

You will need to make an Application in HAL in order to push this infrastructure. Below are steps on configuring this.

1. From the **Apps** page on HAL, click on **Add Application**
2. Fill out the following fields
    1. **Name -**you can use a format like **{ApplicationName}ServiceMocking.**e.g.: RocketMortgageServiceMocking
    2. **Organization -** An Organization in HAL containers the credentials for your AWS account(s), so select the organization that has the accounts tied to it you wish to push to. e.g.: Client Driven Experiences
    3. **GitHub Enterprise Repository** - Enter either your forked starter kit URL or if you made a custom repository, use that URL. e.g.: [https://git.rockfin.com/RocketMortgage/ServiceMocking.git](https://git.rockfin.com/RocketMortgage/ServiceMocking.git)
    4. **Provider** - Select **AWS**
    5. **Platform** - Can leave blank
    6. **Language** - Can leave blank

**<ac:image ac:height="250"><ri:attachment ri:filename="image2019-1-29_9-27-15.png"></ri:attachment></ac:image>**
3. Open the application and click **Manage Application.**Then scroll down and click **Manage Deployment Configuration**. Click **Manually Add Deployment Target**
4. Under AWS, choose the environment you created your infrastructure in (e.g.: test-aws), and fill out the following fields:
    1. **Name** - Can be left blank, but you can enter a helpful friendly name (e.g: Mock or Service Mocking)
    2. **Script Context** - Enter the **region name** that your infrastructure lives in. If you used the default options in the infrastructure setup steps, you can just enter **us-east-2**
    3. **Credentials** - Choose the NonProd deployment credentials for your account (e.g.: **Rocket Mortgage - NonProd (AWS Role)
<ac:image ac:height="400"><ri:attachment ri:filename="image2019-1-29_9-35-40.png"></ri:attachment></ac:image>**
5. Click**Save Changes**


## What's Next

For the next steps, We'll be updating the CircleCI and HAL yml files with the correct information. Before continuing, make note of the following:

- Hal Application ID of the application we made above
- Deployment Target ID of the deployment target we configured above.


If you are viewing the deployment target, you can get both of these values from the URL

<ac:image ac:height="400"><ri:attachment ri:filename="2019-01-29_9-37-40.png"></ri:attachment></ac:image>


