# amazon-ec2-by-ssm-association

## deploy

```sh
aws cloudformation create-stack \
    --stack-name amazon-ec2-by-ssm-association \
    --capabilities CAPABILITY_IAM \
    --template-body file://template.yaml
```

## undeploy

```sh
BUCKET_NAME=$(aws cloudformation describe-stacks \
    --stack-name amazon-ec2-by-ssm-association \
    --query 'Stacks[].Outputs[?OutputKey==`SSMAssocLogs`].OutputValue' \
    --output text)

aws s3 rm s3://${BUCKET_NAME} --recursive
```

```sh
aws cloudformation delete-stack \
    --stack-name amazon-ec2-by-ssm-association
```
