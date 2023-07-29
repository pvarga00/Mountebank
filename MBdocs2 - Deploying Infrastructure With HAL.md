
## Overview

In this section, we will go over the process of deploying your infrastructure with HAL
<ac:structured-macro ac:name="info" ac:schema-version="1" ac:macro-id="79a3f20a-bdc3-422d-b028-2c89101baa7b"><ac:rich-text-body><p>This is&nbsp;<strong>part 2</strong>&nbsp;of a series of configuring your instance of Mountebank. <ac:link><ri:page ri:content-title="Mountebank: Getting Mountebank Up And Running in AWS"></ri:page><ac:plain-text-link-body><![CDATA[Please reference the entrypoint to follow the guide]]></ac:plain-text-link-body></ac:link></p></ac:rich-text-body></ac:structured-macro>
Now that both our HAL application is configured and we've made the necessary changes to our infrastructure files, we can new setup and deploy our infrastructure

1. Go into your application in HAL, and click **Edit Application**. Make sure that **Inject read-only AWS credentials into non-prod builds** is enabled. Under **Parameterized Builds / Deployments** , add the following two items to **Required Build Parameters: module, region.**Click **Save Changes**
**<ac:image ac:height="400"><ri:attachment ri:filename="image2019-1-28_10-57-43.png"></ri:attachment></ac:image>**
2. Click on**Manage Deployment Configuration**and click **Manually Add Deployment Target**
<ac:image ac:height="127"><ri:attachment ri:filename="image2019-1-28_11-5-22.png"></ri:attachment></ac:image>
3. Under **AWS** , select the environment you wish to deploy to (based on what your environment folder is set to from the infrastructure repository steps). For example, the default is **test**, so you would select **test-aws
<ac:image ac:height="400"><ri:attachment ri:filename="image2019-1-28_11-6-48.png"></ri:attachment></ac:image>**
4. Select the following values:

    1. **Server or Service Type -**Select **Script**
    2. **Script Context** - Enter **ecs-app** . This refers to the module you wish to deploy (which there is only one in this case)
    3. **Credentials** - Select the **Non-Prod IAC** credentials for your organization. For example, CDE's is **Client Driven Experiences - NonProd - IAC (AWS Role)**<ac:image ac:height="400"><ri:attachment ri:filename="image2019-1-28_11-28-8.png"></ri:attachment></ac:image>
5. Click **Add Deployment ,**then click **Application Dashboard**.
6. We can now build and deploy. Click **Start New Build**. Make sure **test-aws** is checked. Select **master** for the Source. Under Build Parameters, set **module** to ecs-app, and set **region** to the region you wish to deploy this infrastructure to (if you aren't sure - use **us-east-2**). Click **Start Build**.

<ac:image ac:height="400"><ri:attachment ri:filename="image2019-1-28_11-30-37.png"></ri:attachment></ac:image>
7. You build will perform a **terraform plan** to determine what infrastructure needs to be added. Once the build is done, you can inspect the output to determine what it will generate. **There should only be additions**. If you see anything changing or deleting, something is not configured correctly in your HAL configuration or Infrastructure files.

<ac:image ac:height="400"><ri:attachment ri:filename="image2019-1-28_11-33-8.png"></ri:attachment></ac:image>
8. Once you have validated that the plan looks correct, you can click **Deploy Build**at the top to begin the deployment process. On the next page, check the **Push Infrastructure** checkbox on**ecs-app**, then click **Push To Selected Servers**
<ac:structured-macro ac:name="info" ac:schema-version="1" ac:macro-id="2e6a111d-7305-4220-8fae-b8e27a12fd35"><ac:rich-text-body><p>In order to push this infrastructure, the user pushing it will need to be an<strong>Infrastructure Administrator for Non-Prod </strong>in HAL</p></ac:rich-text-body></ac:structured-macro>    **<ac:image ac:height="250"><ri:attachment ri:filename="image2019-1-29_9-15-47.png"></ri:attachment></ac:image>

<ac:image ac:height="250"><ri:attachment ri:filename="image2019-1-29_9-16-10.png"></ri:attachment></ac:image>**
9. The push process will take some time, but once it is done, you should see an output of the ARNs for the infrastructure pieces it created.

<ac:image ac:height="221"><ri:attachment ri:filename="image2019-1-29_9-18-29.png"></ri:attachment></ac:image>


## Next Steps

For the next part of this process, make note of the following items:

- **ecs\_task\_name**



