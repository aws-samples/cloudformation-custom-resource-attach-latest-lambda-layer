# Attach Lambda Layer CloudFormation Custom Resource (CFNAttachLambdaLayer)

## Purpose

[AWS CloudFormation](https://aws.amazon.com/cloudformation/) does not support referencing "the latest version" of a layer when creating a Lambda function.
This becomes problematic when the layer was created outside of your CloudFormation template.

CFNAttachLambdaLayer  allows you to specify a Lambda and the Layer name that will be attached to it.
It will attach the latest version of the Layer to the specified Lambda.


## Requirements

- The [AWS CLI](https://www.python.org/downloads/)
- The [AWS Serverless Application Model](https://docs.aws.amazon.com/serverless-application-model/index.html) must be [installed](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/serverless-sam-cli-install.html)
- [Python 3.7](https://www.python.org/downloads/)

## Deploying CFNAttachLambdaLayer

From the command line, run:

```bash
sam build -t ./cfn_attach_lambda_layer.yml
sam deploy  --template-file .aws-sam/build/template.yaml --stack-name cfn_attach_lambda_layer  --capabilities "CAPABILITY_NAMED_IAM" --resolve-s3
```

This will deploy an AWS Lambda custom resource that can be called by your CloudFormation template.

## Usage

```yaml
  AttachLayer:
    Type: Custom::LayerAttachment
    Properties:
      LayerName: <Your Layer name>
      LambdaName: <Lambda name or ARN>
      ServiceToken: !ImportValue CFNAttachLambdaLayer
```
