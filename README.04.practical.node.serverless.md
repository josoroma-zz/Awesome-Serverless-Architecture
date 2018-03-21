# Serverless Node with AWS Lambda

- https://github.com/azat-co/practicalnode/blob/master/chapter16/chapter16.md

Set up a REST API using Lambda to access and perform CRUD on tables in your noSQL DynamoDB database. Lambdas are charged only when they are working unlike EC2 instances which are charged for always, as long as they are running. This way with Lambda, your company will pay only for peaks and in other times when there's 0 traffic, it won't be charged at all! Stales news get almost no traffic.

Let's learn how to get started with Lambda by building a REST API for any database tables not just one. 

You are going to use three Amazon Web Services (AWS) services which we will cover in this chapter:

- DynamoDB
- Lambda
- API Gateway