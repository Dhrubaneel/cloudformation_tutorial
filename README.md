# Cloudformation Tutorial

This repo contains code to create a basic cloudformation stack and deploy it using AWS Cli.

## User Story

Assume there is an application named News_Board, which collects news from different third party News_Reporter applications and show in one place. News_Board has an api open which News_Reporters use to send data to News_Board via HTTP POST call. Apart from showing the data in one place, News_Board stores all input data as a backup and reference for future.

## Technical Architecture

There will be one Aws Api Gateway which can be called from Postman to pass data. Api Gateway should be connected to a Kinesis stream. A Firehose should be there to take the data from Kinesis stream and store that in a S3 bucket.

The AWS resources used are 
    1) api gateway
    2) kinesis
    3) firehose
    4) s3
    
Note: This repo only creates S3 and Kinesis and not the full implementation as this is only for giving a basic idea about how things work

## Vital Commands

### Create Stack
`aws cloudformation create-stack --stack-name cf-tutorial --template-body file://deploy.yaml --parameters file://params.json --capabilities CAPABILITY_AUTO_EXPAND`

### Update Stack
`aws cloudformation update-stack --stack-name cf-tutorial --template-body file://deploy.yaml --parameters file://params.json --capabilities CAPABILITY_AUTO_EXPAND`

### Delete Stack
`aws cloudformation delete-stack --stack-name <stack name>`

### Validate a stack
`aws cloudformation validate-template --template-body file://deploy.yaml`

### Check status of stacks
`aws cloudformation describe-stacks`

### List stacks
`aws cloudformation list-stacks`

## Note
When integrating CloudFormation into CI/CD pipeline we need to create a CloudFormation stack on the first run of the pipeline, while  need to update the stack for all following pipeline runs. If we use the AWS CLI this is painful.

Node module cfn-create-or-update can create or update a CloudFormation stack. If no updates are to be performed, no error is thrown. cfn-create-or-update behaves exactly as the AWS CLI regarding input values, output will be different.

### Installation
`npm install -g cfn-create-or-update`

### To create or update a stack, run:
`cfn-create-or-update --stack-name cf-tutorial --template-body file://deploy.yaml --parameters file://params.json --capabilities CAPABILITY_AUTO_EXPAND --region ap-south-1`

