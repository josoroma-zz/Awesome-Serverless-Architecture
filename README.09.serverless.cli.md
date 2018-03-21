# Serverless AWS Lambda CLI Reference

Using the **AWS Management Console**:

- https://docs.aws.amazon.com/lambda/latest/dg/get-started-create-function.html

Using `Serverless CLI`:

- https://github.com/serverless/serverless

- https://serverless.com/framework/docs/providers/aws/cli-reference

- https://github.com/serverless/serverless/tree/master/docs/providers/aws/cli-reference

## Create service in current working directory

```
serverless create --template aws-nodejs
```

## Create service in new folder:

```
serverless create --template aws-nodejs --path myService
```

## Create service in new folder using a custom template

```
serverless create --template-url https://github.com/serverless/serverless/tree/master/lib/plugins/create/templates/aws-nodejs --path myService
```

## Available templates for Node

- https://serverless.com/framework/docs/providers/aws/cli-reference/create#available-templates

```
aws-nodejs
aws-nodejs-typescript
aws-nodejs-ecma-script
```

### Creating a new plugin

- https://serverless.com/framework/docs/providers/aws/cli-reference/create#creating-a-new-plugin

To generate the scaffolding for a hello world plugin that demonstrates how to create a new command and how to listen to the various events available.

```
serverless create --template plugin
```

## AWS - Logs

- https://serverless.com/framework/docs/providers/aws/cli-reference/logs

## Examples

Serverless Examples – A collection of boilerplates and examples of serverless architectures built with the Serverless Framework and AWS Lambda.

- https://github.com/serverless/examples

## How to Make a Serverless GraphQL API using Lambda and DynamoDB

- https://serverless.com/blog/make-serverless-graphql-api-using-lambda-dynamodb

### GraphQL query endpoint in NodeJS on AWS with DynamoDB

Let's see how easy it is to use GraphQL with the Serverless Framework:

- https://github.com/serverless/examples/tree/master/aws-node-graphql-api-with-dynamodb

## Serverless GraphQL Examples for AWS AppSync and Apollo

- https://github.com/serverless/serverless-graphql

Part 1: This post! GraphQL endpoints with API Gateway + AWS Lambda:

- https://serverless.com/blog/running-scalable-reliable-graphql-endpoint-with-serverless

Part 2: AppSync Backend: AWS Managed GraphQL Service:

- https://hackernoon.com/running-a-scalable-reliable-graphql-endpoint-with-serverless-24c3bb5acb43

## Create a Node REST API with Express.js

- https://serverless.com/blog/serverless-express-rest-api

We will:

- Deploy a simple API endpoint.
- Add a DynamoDB table and two endpoints to create and retrieve a User object.
- Set up path-specific routing for more granular metrics and monitoring.
- Configure your environment for local development for a faster development experience.