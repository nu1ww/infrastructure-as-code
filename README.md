# Boilerplate - Cloudformation


### AWS Cloudformation Templates

According to proposed architecture had been completely designed with AWS cloudformation. Entire architecture components were modularized in to separate files to improve the maintainability and readability. So please execute these templates based on  the following sequence, 
- **01-vpc.yml** - Generate base VPC 
- **02-iam.yml** - ECS related IAM role
- **03-ecs-cluster.yml** - Fargate Cluster
- **04-ecr.yml** - ECR for BackOffice ECS service
- **05-ecs-service.yml** - BackOffice ECS service
- **06-sqs.yml** - SQS for queueing input messages
- **07-rds.yml** - RDS instance for store user/ org related information

### Create CloudFormation Stacks Using AWS CLI

```
aws cloudformation create-stack --template-body file://$PWD/01-vpc.yml --stack-name mas-sp-prod-vpc --parameters ParameterKey=AppName,ParameterValue="mas-spryng" ParameterKey=Env,ParameterValue=prod

aws cloudformation create-stack --template-body file://$PWD/02-iam.yml --stack-name mas-sp-prod-iam --parameters ParameterKey=AppName,ParameterValue="mas-spryng" ParameterKey=Env,ParameterValue=prod --capabilities CAPABILITY_NAMED_IAM

aws cloudformation create-stack --template-body file://$PWD/03-ecs-cluster.yml --stack-name mas-sp-prod-app-cluster --parameters ParameterKey=AppName,ParameterValue="mas-spryng" ParameterKey=Env,ParameterValue=prod

aws cloudformation create-stack --template-body file://$PWD/04-ecr.yml --stack-name mas-sp-prod-ecr --parameters ParameterKey=ServiceName,ParameterValue="mas-spryng" ParameterKey=Env,ParameterValue=prod

aws cloudformation create-stack --template-body file://$PWD/05-ecs-service.yml --stack-name mas-sp-prod-api-service --parameters ParameterKey=ServiceName,ParameterValue="mas-spryng" ParameterKey=Env,ParameterValue=prod

<!-- aws cloudformation create-stack --template-body file://$PWD/06-sqs.yml --stack-name sqs-queues --parameters ParameterKey=AppName,ParameterValue="mas-spryng" ParameterKey=Env,ParameterValue=<ENVIRONMENT> -->

aws cloudformation create-stack --template-body file://$PWD/07-rds.yml --stack-name mas-sp-prod-rds --parameters ParameterKey=Project,ParameterValue="mas-spryng" ParameterKey=Env,ParameterValue=prod ParameterKey=MasterUsername,ParameterValue="admin" ParameterKey=MasterUserPassword,ParameterValue=BBOXDRJsopEWj3LB
```
### Login to AWS IAM Using CLI
```
export AWS_ACCESS_KEY_ID=<KEY> && export AWS_SECRET_ACCESS_KEY=<ACCESS_KEY> && export AWS_DEFAULT_REGION=us-east-1
```
