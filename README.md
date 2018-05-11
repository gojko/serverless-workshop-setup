# Serverless workshop setup

This page outlines how to set up your machine to attend Gojko's serverless coding workshop. It's very important to do this upfront so that we can use the time together effectively. Expect the setup to take 10-20 minutes, and contact gojko@neuri.co.uk before the workshop if you're having trouble with any of the tests below.

## Basic software required

* [Node.js](https://nodejs.org) 6 or 8
* [NPM](http://npmjs.com/) 3 or higher
* [AWS Command line tools](https://aws.amazon.com/cli/)
* a code editor (any will do, but something with JavaScript support will speed things up)

## Setup your AWS account

Register for an AWS account upfront if you don't already have one. To use Lambda, you'll need a verified account (typically using phone verification). The stuff we'll do will fit into the free account allowance, so you will not need to pay AWS anything for the workshop, but you will still need an account. Register at [aws.amazon.com/](https://aws.amazon.com)

If you do not want to use the access credentials for your main user account, but want to set up a separate user profile for the camp, assign the following roles to the user:

  * [arn:aws:iam::aws:policy/IAMFullAccess](https://console.aws.amazon.com/iam/home?region=us-east-1#policies/arn:aws:iam::aws:policy/IAMFullAccess) 
  * [arn:aws:iam::aws:policy/PowerUserAccess](https://console.aws.amazon.com/iam/home?region=us-east-1#policies/arn:aws:iam::aws:policy/PowerUserAccess)
 
If you have a company AWS account and intend to use it during the workshop, please make sure that you have access rights specified above.

## Set up AWS Command line tools

Configure AWS Command Line tools to [work with your credentials](http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html). If you do not want to use your primary account, [set up a separate profile](https://docs.aws.amazon.com/cli/latest/userguide/cli-multiple-profiles.html) for the workshop account.

## Test your AWS setup

The following commands should all work OK, without throwing errors (add `--profile <PROFILE NAME>` to the commands if you want to use a specific profile for AWS access):

1. Set up a simple IAM role (get the [policy.json](policy.json) file from this repository and put it in the local directory where this command is executed)

```bash
aws iam create-role --role-name=hello-world-role --assume-role-policy-document file://policy.json --query Role.Arn --output text
```

2. Wait about 10 seconds, then use the result printed by the previous command instead of `<ROLE>` in the command below, to set up a simple Lambda function (get the [test-lambda.zip](test-lambda.zip) file from this repository and put it in the local directory where this command is executed).

```bash
aws lambda create-function --function-name hello-world-function --role <ROLE> --runtime nodejs8.10 --handler main.handler --zip-file fileb://test-lambda.zip 
```

3. set up a simple API interface:

```bash
aws apigateway create-rest-api --name test-api
```
