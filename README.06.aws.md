# AWS Lambda

- AWS Lambda lets you run code without provisioning or managing servers

- We pay only for the compute time we consume.

## AWS documentation on GitHub

- https://aws.amazon.com/de/blogs/aws/aws-documentation-is-now-open-source-and-on-github

- https://github.com/awsdocs

## Supported Node.js runtimes:

- https://docs.aws.amazon.com/lambda/latest/dg/programming-model.html

  - Node.js runtime v6.10 (runtime = nodejs6.10)
  - Node.js runtime v4.3 (runtime = nodejs4.3)
  - Node.js runtime v0.10.42 (runtime = nodejs)

### Create a lambda function

 Using the **AWS Management Console:**

- https://docs.aws.amazon.com/lambda/latest/dg/get-started-create-function.html

- https://hackernoon.com/a-crash-course-on-serverless-with-node-js-632b37d58b44

```
serverless create --template aws-nodejs --path my-service
```

### The lambda function handler

At the time you create a Lambda function you specify a handler, a function in your code, that AWS Lambda can invoke when the service executes your code.

- https://docs.aws.amazon.com/lambda/latest/dg/nodejs-prog-model-handler.html

```
exports.myHandler = function(event, context, optionalCallback) {
  // event – To pass in event data to the handler.
  // context – To provide Our handler the runtime information of the Lambda function that is executing.
  // callback – We can use the optional callback to return information to the caller, otherwise return value is null.
}
```

for example:

```
exports.myHandler = function(event, context, callback) {
  // The console.log() statements log some of the incoming event data to CloudWatch Logs.
  console.log("value1 = " + event.key1);
  console.log("value2 = " + event.key2);
  callback(null, "some success message"); // or callback("some error type"); 
}
```

The following are example callbacks:

```
callback();     // Indicates success but no information returned to the caller.
callback(null); // Indicates success but no information returned to the caller.
callback(null, "success");  // Indicates success with information returned to the caller.
callback(error);    //  Indicates error with error information returned to the caller.
```

### The Context Object

While a Lambda function is executing, it can interact with AWS Lambda to get useful runtime information such as:

- How much time is remaining before AWS Lambda terminates your Lambda function (timeout is one of the Lambda function configuration properties).

- The CloudWatch log group and log stream associated with the Lambda function that is executing.

- The AWS request ID returned to the client that invoked the Lambda function. You can use the request ID for any follow up inquiry with AWS support.

- If the Lambda function is invoked through AWS Mobile SDK, you can learn more about the mobile application calling the Lambda function.

```
console.log('Loading function');

exports.handler = function(event, context, callback) {
    //console.log('Received event:', JSON.stringify(event, null, 2));
    console.log('value1 =', event.key1);
    console.log('value2 =', event.key2);
    console.log('value3 =', event.key3);
    console.log('remaining time =', context.getRemainingTimeInMillis());
    console.log('functionName =', context.functionName);
    console.log('AWSrequestID =', context.awsRequestId);
    console.log('logGroupName =', context.logGroupName);
    console.log('logStreamName =', context.logStreamName);
    console.log('clientContext =', context.clientContext);
    if (typeof context.identity !== 'undefined') {
        console.log('Cognito
        identity ID =', context.identity.cognitoIdentityId);
    }    
    callback(null, event.key1); // Echo back the first key value
    // or
    // callback("some error type"); 
};
```

The handler code in this example logs some of the runtime information of the Lambda function to CloudWatch. If We invoke the function using the Lambda console, the console displays the logs in the Log output section. We can create a Lambda function using this code and test it using the console.

https://docs.aws.amazon.com/lambda/latest/dg/get-started-create-function.html

### AWS Lambda logs on CloudWatch

- https://docs.aws.amazon.com/lambda/latest/dg/nodejs-prog-model-logging.html
    
##  AWS SAM Local, a CLI Tool to Test AWS Lambda Functions Locally

- https://docs.aws.amazon.com/lambda/latest/dg/test-sam-local.html

- https://docs.aws.amazon.com/lambda/latest/dg/sam-cli-requirements.html

- https://github.com/awslabs/aws-sam-local

## AWS Serverless Application Model (AWS SAM)

Prescribes rules for expressing Serverless applications on AWS.

- https://github.com/awslabs/serverless-application-model

How to create serverless applications using AWS SAM:

- https://github.com/awslabs/serverless-application-model/blob/master/HOWTO.md

Detailed instructions on how to write AWS SAM templates and deploy them to AWS CloudFormation:

- https://github.com/awslabs/serverless-application-model/tree/master/examples
