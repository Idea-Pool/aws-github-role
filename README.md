# aws-github-role

This project contains a CloudFormation template that creates an IAM role for GitHub Actions. The role has specific policy statements and a trusted relationship as defined in the template.

## Template Details

The template takes two input parameters:

- `GitHubAccount`: The GitHub account name

The template creates a role with the following policy statements:

- `iam:PassRole` on all resources
- `sts:AssumeRole` on all `cdk-*` roles

The role has a trusted relationship with the GitHub Actions OIDC provider.

The template has two outputs:

- `RoleArn`: The ARN of the GitHub role
- `RoleName`: The name of the GitHub role

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