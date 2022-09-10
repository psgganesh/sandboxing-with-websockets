# Step 1: Setting up the backend using SAM CLI

## Install and configure the SAM CLI
### What is AWS SAM?
AWS SAM is short for Serverless Application Model. It is an open-source project that helps create and deploy serverless apps on AWS.

AWS SAM has multiple components. Today, we'll be covering 2 things in high level, just to give you a taste.

#### 1. SAM Template
A SAM template helps you write serverless resource configuration really fast. It is like CloudFormation, but supercharged. When deploying, SAM template "transforms" itself into a CloudFormation template before deploying just like a regular CloudFormation template. Today will go through a SAM template in a high level.

#### 2. SAM CLI
The SAM CLI is a tool to get you started with SAM based applications really quickly. As a developer, it helps you with bootstrapping, building, testing, and deploying. Today, we'll be going through a few of these things.

AWS SAM provides you with a command line tool, the AWS SAM CLI, that makes it easy for you to create and manage serverless applications. You need to install and configure a few things in order to use the AWS SAM CLI.

To install the AWS SAM CLI, see the following instructions for your development host:

- [Installing the AWS SAM CLI on Linux](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install-linux.html)
- [Installing the AWS SAM CLI on Windows](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install-windows.html)
- [Installing the AWS SAM CLI on macOS](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install-mac.html)

##### What are we building ?
We will be creating 
- 3 Lambda functions
- 1 DynamoDB table
- 1 APIGateway Websockets API
```
.
├── onconnect                   <-- Lambda Source code onconnect
├── ondisconnect                <-- Lambda Source code ondisconnect
├── onsend                      <-- Lambda Source code onsend
└── template.yaml               <-- SAM template for Lambda Functions and DDB
```

##### AWS SAM CLI commands

If you prefer, you can install the [AWS SAM CLI](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html) and use it to package, deploy, and describe your application.  These are the commands you'll need to use:

#### 3. Clone this repository onto local
```shell
git clone https://github.com/psgganesh/sandboxing-with-websockets.git
git checkout step1
```
#### 4. Deploy the backend resources with a single command
SAM CLI deploys the following resources
- 1 Websocket API on Amazon APIGateway
- 3 AWS Lambda functions
- 1 Amazon DynamoDB table

```shell
cd sam
sam deploy --guided
```

1. For Stack name, enter api.
2. For AWS Region, `hit return key` to select the default.
3. For Confirm changes before deploy, `hit return key` to select the default.
4. For Allow SAM CLI IAM role creation, `hit return key` to select the default.
5. For Disable rollback, enter the `N` -> This will ensure CloudFormation will rollback in case of any errors
6. For Save arguments to configuration file, `hit return key` to select the default.
7. For SAM configuration file, `hit return key` to select the default.
8. For SAM configuration environment, `hit return key` to select the default.
9. For Deploy this changeset? enter `y`.

Once the backend is deployed look for the Key `WebSocketURI` and copy the `Value` of the key. 

It should start with `wss://`. We will use this key later when we use the frontend.

**Note:** `.gitignore` contains the `samconfig.toml`, hence make sure backup this file, or modify your .gitignore locally.

### Credits for this SAM template
This SAM template is a modified version of the SAM template which is referred from [AWS Blog](https://aws.amazon.com/blogs/compute/announcing-websocket-apis-in-amazon-api-gateway/)