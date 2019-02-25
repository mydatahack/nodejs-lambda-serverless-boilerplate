# nodejs-lambda-serverless-boilerplate

**Boilerplate to create AWS Lambda Function with Node.js and deploy it with Serverless**

Boilerplate for Node.js lambda function, including Serveless configuration, JavaScript function, and unit test examples. 

This example lambda function make a get request to external api endpoint and return the result through the API gateway endpoint. The function runs in the default VPC.

## What can I do with this boilerplate

1. Create Node.js lambda function with unit & integration tests (using mocha).
2. Unit testing code coverage report (using istanbul).
3. Deployment with Serverless command.
4. Serverless configuration includes: 
  * Create API gateway with custom endpoint.
  * Run Lambda function in a specific VPC and a group of subnets.
  * Assign IAM Roles to the function.
  * Create AWS resources that are associated with the function.


## (1) Serverless installation
Using [serverless](https://serverless.com/) framework to package & deploy lambda function. Install serverless globally as below.

```bash
npm install serverless -g
```

## (2) Package installation

Run the command below to install all the packages

```bash
npm i
```

## (3) Deployment

Deployment can be done through the local machine by running Serverless command. For production, it is recommended to use a CD/CI tool like Jenkins. AWS CLI must be configured with the appropriate credental.

```bash
sls deploy --stage dev
```

## (4) Unit testing and code coverage

Using Mocha for unit testing and Istanbul for code coverage.

Run the command below to perform unit test

```base
npm test
```

## (5) Calling endpoint

The endpoint will be output in Jenkins console after deployment completes. It is a simple get request. You can call it with curl or web browser.

Endpoint looks like: https://somekindofuniqueidyouget.execute-api.ap-southeast-2.amazonaws.com/dev/nodejs-lambda-boilerplate

Upon deployment check for the deployment message as below.

```
Serverless: Packaging service...
Serverless: Excluding development dependencies...
Serverless: Uploading CloudFormation file to S3...
Serverless: Uploading artifacts...
Serverless: Uploading service .zip file to S3 (10.87 MB)...
Serverless: Validating template...
Serverless: Creating Stack...
Serverless: Checking Stack create progress...
.............................
Serverless: Stack create finished...
Service Information
service: nodejs-lambda-boilerplate
stage: dev
region: ap-southeast-2
stack: nodejs-lambda-boilerplate-dev
api keys:
  None
endpoints:
  GET - https://somekindofuniqueidyouget.execute-api.ap-southeast-2.amazonaws.com/dev/nodejs-lambda-boilerplate
functions:
  nodejsLambdaBoilerPlate: nodejs-lambda-boilerplate-dev-nodejsLambdaBoilerPlate
```

## How did the boilerplate get created?

This section explains how the boilerplate was created.

Initialise with npm init

```bash
npm init -y

```

Create a new AWS lambda service using the Node.js template. This create a boilerplate with .gitignore, handler.js and serverless.yml files.

```bash
serverless create --template aws-nodejs --path serverless
```

Create folders and files

```
  - config
    - certs.yml (Certificate names per environment)
    - domains.yml (Domain names and base path for API endpoint. The record will be created by Route53)
    - env.yml (Environment variables set in the lambda execution environememt. Example includes environment and parameter names for db connections)
    - permissions.yml (Defines what lambda function is permitted to do. Example includes access rights to parameter store)
    - resources.yml (Resources you want to create along with lambda function. Example includes alerts.)
    - vpc
      - uat1.yml (Including Security group ids and subnet ids where you want to run the lamda function.)
      - tst1.yml
      - prd1.yml
  - src
    - handler.js
    - dataProcessor.js
    - exampleData.js
  - test
    - handler.spec.js
    - dataProcessor.spec.js

```

Installing dependencies as in package.json

```
npm install
```