<p align="center">
  <img src="https://miro.medium.com/max/1400/1*bImkauctDDwzT5bOa51MEQ.png" width="350" title="hover text">
  <img src="your_relative_path_here_number_2_large_name" width="350" alt="accessibility text">
</p>

# AWS S3 Deploy GitHub Action with Self Runner
Here we use our oun self runner that installed on ec2 then we use that runner to upload our github static website in s3 bucket



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
change the variable as according your variable
