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