# amazonconnect-exportagents
This solution allows you to export the agents in Amazon Connect and their relevant details, such as security profiles, routing profiles queues etc in csv format, stores them in S3 bucket, this can then either be downloaded manually or can be integrated with Lambda and SES to send you the attachment.

#Solution:

#We use amazon connect APIs in our Python Lambda code called, BulkExportAgentsLambda function to list all agents, then describe the attributes of that agent example, what is the routing profile of the agent, security profile of the agent, queues assosciated in their routing profile, ACW time etc.

#We then write those details to CSV file and store it in the S3 bucket.

#We can then export that CSV file from S3 bucket using another Lambda, called emailAttachmentLambda.
#emailAttachmentLambda- This is triggered by the PUT event type in S3, with suffix .csv and prefix /tmp folder.

#Or We can manually download the file from S3 bucket.

#We will then define a rule on event bridge to trigger the first lambda function on a schedule.

Please Note: For this solution to work, make sure your Lambda code has relevant read/write permissions to S3,SES,AWS Connect etc, otherwise your Lambda Execution will fail. Also increase the time out if long list of agents in your contact center. Additionally the pagination settings has to be modified for extremely high API calls.

This solution can be customized as per your needs further, by modifying the codes.


# For all troubleshooting steps if Lambda throws any error, please check the cloudwatch log group and check relevant logs.
Most common errors:
Permission Denied errors: Make sure you have provided IAM role of Lambda relevant permissions like reading files from S3, getting agent list and describing attributes in AWS Connect.
Timeout Errors- Make sure your Lambda has enough time out to run properly, and adjust as per your agents in contact center.
