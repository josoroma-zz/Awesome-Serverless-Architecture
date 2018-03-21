# Serverless Web Application Workshop

- https://github.com/awslabs/aws-serverless-workshops/tree/master/WebApplication

The application architecture uses:

- AWS Lambda
- Amazon API Gateway
- Amazon S3
- Amazon DynamoDB
- Amazon Cognito.

**Amazon S3** hosts static web resources including HTML, CSS, JavaScript, and image files which are loaded in the user's browser. 

JavaScript executed in the browser sends and receives data from a public backend API built using **AWS Lambda** and **Amazon API Gateway**. 

**Amazon Cognito** provides user management and authentication functions to secure the backend API.

Finally, **Amazon DynamoDB** provides a persistence layer where data can be stored by the API's Lambda function.