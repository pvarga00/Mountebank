
## Overview

In this section, we will go over the process configuring CircleCI, which will build & deploy Mountebank
<ac:structured-macro ac:name="info" ac:schema-version="1" ac:macro-id="79a3f20a-bdc3-422d-b028-2c89101baa7b"><ac:rich-text-body><p>This is&nbsp;<strong>part 5</strong>&nbsp;of a series of configuring your instance of Mountebank. <ac:link><ri:page ri:content-title="Mountebank: Getting Mountebank Up And Running in AWS"></ri:page><ac:plain-text-link-body><![CDATA[Please reference the entrypoint to follow the guide]]></ac:plain-text-link-body></ac:link></p></ac:rich-text-body></ac:structured-macro>


## Configuring CircleCI

Now that all the pieces are in place, we can do the final configuration of CircleCI, which will build and deploy Mountebank

1. Go to [https://circleci.foc.zone](https://circleci.foc.zone/) and **select the Organization your Mountebank repository is in at the top-left

<ac:image ac:height="400"><ri:attachment ri:filename="image2019-1-29_10-17-56.png"></ri:attachment></ac:image>**
2. Click**Add Projects**, and click **Set Up Project** under your Mountebank repository. Then click **Start building**

<ac:image ac:height="250"><ri:attachment ri:filename="image2019-1-29_10-19-58.png"></ri:attachment></ac:image>
<ac:image ac:height="400"><ri:attachment ri:filename="image2019-1-29_10-20-37.png"></ri:attachment></ac:image>
3. This will begin the build process. **Note that because we have not configured our AWS credentials in the job properties, the job will fail.**To add these credentials, click on the **gear icon** at the top-right of your job. Click **AWS Permissions** and enter in your Access Key ID and Secret Access Key, then click **Save AWS keys**


You'll now need to start a new job for these changes to apply. You can do this by selecting **Workflows**, selecting the Mountebank application, then clicking **Rerun→Rerun from Beginning** under the latest job

<ac:image ac:height="400"><ri:attachment ri:filename="image2019-1-29_10-31-6.png"></ri:attachment></ac:image>

Once the job starts, it will both create a build and deployment in HAL and deploy the code automatically. Once the circle job is done, you can validate that it deployed by going into the application in HAL and seeing the Last push as a success.

<ac:image ac:height="250"><ri:attachment ri:filename="image2019-1-29_10-32-31.png"></ri:attachment></ac:image>
