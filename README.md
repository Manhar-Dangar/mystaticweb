# AWS S3 Deploy GitHub Action with Self Runner
Here we use our oun self runner that installed on ec2 then we use that runner to upload our github static website in s3 bucket

<p align="center">
  <img src="https://miro.medium.com/max/1400/1*bImkauctDDwzT5bOa51MEQ.png" width="100%">
</p>


## First What you need to do
1. Go to the your github account then setting >> Action >> runner choose your runner op.
then install the runner by using the command that provided by github.  
2. configure your aws account in runner  
3. now make the yaml pipeline

## Paste below pepline code
```
name: Upload Website

on:
  push:
    branches:
    - main

jobs:
  deploy:
    runs-on: self-hosted
    steps:
    - uses: actions/checkout@main
    - run: |
           aws s3 ls
           ls
           pwd
           aws s3 cp index.html "${{ secrets.AWS_S3_BUCKET }}"
```     
## Configuration
change the variable as according your secret variable

| Key | Value | Suggested Type | Required | Default |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| `AWS_ACCESS_KEY_ID` | Your AWS Access Key. [More info here.](https://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) | `secret env` | **Yes** | N/A |
| `AWS_SECRET_ACCESS_KEY` | Your AWS Secret Access Key. [More info here.](https://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html) | `secret env` | **Yes** | N/A |
| `AWS_S3_BUCKET` | The name of the bucket you're syncing to. For example, `jarv.is` or `my-app-releases`. | `secret env` | **Yes** | N/A |
| `AWS_REGION` | The region where you created your bucket. Set to `us-east-1` by default. [Full list of regions here.](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-available-regions) | `env` | No | `us-east-1` |
| `AWS_S3_ENDPOINT` | The endpoint URL of the bucket you're syncing to. Can be used for [VPC scenarios](https://aws.amazon.com/blogs/aws/new-vpc-endpoint-for-amazon-s3/) or for non-AWS services using the S3 API, like [DigitalOcean Spaces](https://www.digitalocean.com/community/tools/adapting-an-existing-aws-s3-application-to-digitalocean-spaces). | `env` | No | Automatic (`s3.amazonaws.com` or AWS's region-specific equivalent) |
| `SOURCE_DIR` | The local directory (or file) you wish to sync/upload to S3. For example, `public`. Defaults to your entire repository. | `env` | No | `./` (root of cloned repository) |
| `DEST_DIR` | The directory inside of the S3 bucket you wish to sync/upload to. For example, `my_project/assets`. Defaults to the root of the bucket. | `env` | No | `/` (root of bucket) |
