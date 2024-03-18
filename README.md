# aws-github-role

This project contains a CloudFormation template that creates a IAM roles for Idea Pool GitHub Actions. The roles has specific policy statements and a trusted relationship as defined in the template.

## Template Details

The template takes one input parameters:

- `GitHubAccount`: The GitHub account name

The template creates a role for **AWS CDK actions** with the following policy statements:

- `iam:PassRole` on all resources
- `sts:AssumeRole` on all `cdk-*` roles

The template also creates a role for **AWS CLI actions** with the following policies:

- AWS managed policy `AmazonS3FullAccess`
- `cloudformation:GetInvalidation` and `cloudformation:CreateInvalidation` on all resources

The roles have a trusted relationship with the GitHub Actions OIDC provider.

The template has four outputs:

- `GitHubCDKRoleArn`: The ARN of the CDK role
- `GitHubCLIRoleArn`: The ARN of the CLI role
- `GitHubCDKRoleName`: The name of the CDK role
- `GitHubCLIRoleName`: The name of the CLI role

## Deployment

To deploy the CloudFormation stack using the AWS CLI, use the following command:

```bash
aws cloudformation create-stack --stack-name GitHubRoleStack --template-body file://role-template.yaml --parameters ParameterKey=GitHubAccount,ParameterValue=MyGitHubAccount --capabilities CAPABILITY_IAM
```

Replace `MyGitHubAccount` with your actual GitHub account name.

## Outputs

To get the outputs of the stack, use the following command:

```bash
aws cloudformation describe-stacks --stack-name GitHubRoleStack --query "Stacks[0].Outputs" --output text
```

## Destroy

To delete the CloudFormation stack, use the following command:

```bash
aws cloudformation delete-stack --stack-name GitHubRoleStack
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.