# amazon-ec2-by-ssm-association

- CloudFormationでEC2の構築と、EC2内の環境を構築するサンプル
- EC2内に構築する環境は、https://github.com/ot-nemoto/ansible-nginx 参照

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
