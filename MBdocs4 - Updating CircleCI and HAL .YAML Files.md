
## Overview

In this section, we will go over the process of updating your Circle and HAL yml files for build and deployment in HAL
<ac:structured-macro ac:name="info" ac:schema-version="1" ac:macro-id="79a3f20a-bdc3-422d-b028-2c89101baa7b"><ac:rich-text-body><p>This is&nbsp;<strong>part 4</strong>&nbsp;of a series of configuring your instance of Mountebank. <ac:link><ri:page ri:content-title="Mountebank: Getting Mountebank Up And Running in AWS"></ri:page><ac:plain-text-link-body><![CDATA[Please reference the entrypoint to follow the guide]]></ac:plain-text-link-body></ac:link></p></ac:rich-text-body></ac:structured-macro>
## Updating Your CircleCI Yaml

Within the CircleCI yaml, there are a few fields that will need to be updated

1. **CIRCLE\_ECR\_URL** - The format of this URL is**{AWS\_ACCOUNT\_NUMBER}.dkr.ecr.{AWS\_REGION}.[amazonaws.com/{ECS\_TASK\_NAME](http://amazonaws.com/{ECS_TASK_NAME)} .**You will need to replace the bracketed stand ins with the values relevant to your setup. You can use the ECS Task Name obtained from Part 2 of this guide.
2. **CIRCLE\_AWS\_REGION**- **(Optional)** If you are deploying to a region other than us-east-2, update this variable to the appropriate region.
3. **HAL\_APP\_ID**- Set to your HAL Application ID obtained from Part 3
4. **HAL\_TARGETS -**Set to your HAL Deployment Target ID obtained from Part 3


<ac:image><ri:attachment ri:filename="image2019-1-29_9-59-7.png"></ri:attachment></ac:image>

## Updating Your HAL Yaml

You will need to update a few values in your HAL9000 Yaml. Make sure to **update the Yaml at the root of the repository.**

1. **env:**If your deployment target from step 3 is something other than **test-aws**, update the value appropriately.
2. **HAL\_ECS\_CLUSTER** - The format of the cluster name is **{ENVIRONMENT}-ecscluster-{AWS\_ACCOUNT\_NUMBER}-{AWS\_REGION}**. Update the values appropriately.
3. **HAL\_ECS\_TASK** - Use the ECS Task Name obtained from Part 2 of this guide
4. **HAL\_IMAGE\_URL -**The only piece you will need to update is the **{ECS\_TASK\_NAME}****,**which can be set to the value obtained in step 2
5. **HAL\_TASK\_DEFINITION\_NAME**- Use the ECS Task Name obtained from Part 2 of this guide


<ac:image ac:height="250"><ri:attachment ri:filename="image2019-1-29_10-10-37.png"></ri:attachment></ac:image>

Once these changes have been made, make sure to check them in.


