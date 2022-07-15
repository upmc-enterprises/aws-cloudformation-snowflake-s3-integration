# About

This CloudFormation creates an IAM role within an AWS account that allows [Snowflake](https://www.snowflake.com/) to assume.
The configuration deployed makes use of the reference Snowflake document located [here](https://docs.snowflake.com/en/user-guide/data-load-s3-config-storage-integration.html).

### Note
This CloudFormation will provide `["*"]` to the objects within the bucket and does not make use of the S3 Prefix option i.e. `["<path>/*"]` noted in the Snowflake documentation [here](https://docs.snowflake.com/en/user-guide/data-load-s3-config-storage-integration.html#creating-an-iam-policy).

## For KMS Buckets

If you are using an S3 bucket that leverages [AWS KMS](https://aws.amazon.com/kms/) it is required that the KMS key policy has the appropriate permissions to allow the IAM role created access to use the KMS key. If selecting KMS in the deployment options, permission to the designated KMS Key will be granted for the IAM role; however it is still required that the KMS key policy be updated to provide the IAM role access.

## Parameters

| Name | Description |
|:----:|:-----------:|
| SnowflakeRole | The source ARN of the Snowflake role that will be assuming the IAM role in this account. |
| ExternalId | The externalid that is provided by Snowflake when creating an S3 source. |
| Owner | A contact or department of who owns this deployment. |
| Application | The application leveraging Snowlake.  |
| Environment | The application environment.  |
| RoleName | The desired rolename that will be assumed by the Snowflake source role.  |
| AccessLevel | The access level to provide to Snowflake. ReadOnly provides only read access to Snowflake. ReadWrite allows Snowflake to write back to the S3 bucket.  |
| BucketName | The S3 Bucket you wish to give Snowflake access to.  |
| KMSBucket | If the S3 bucket uses KMS CMK select `true`. If you are using AWS managed KMS or AES256 leave `false`.  |
| KMSKey | If KMSBucket was set to `true` then provide the KMS Key ARN of the S3 bucket. |


## Outputs

| Name | Description |
|:----:|:-----------:|
| SnowFlakeAssumeRoleArn | The IAM role that Snowflake is allowed to assume. To be provided back to the Snowflake administrator. |
