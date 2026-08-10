# CI/CD Best Practices — Terraform Infrastructure
 
![CI Pipeline](https://github.com/f-karamizadeh/ce-lab-cicd-best-practices/actions/workflows/ci.yml/badge.svg)
![CD Pipeline](https://github.com/f-karamizadeh/ce-lab-cicd-best-practices/actions/workflows/cd.yml/badge.svg)
![Commit Lint](https://github.com/f-karamizadeh/ce-lab-cicd-best-practices/actions/workflows/commit-lint.yml/badge.svg)
![Release](https://github.com/f-karamizadeh/ce-lab-cicd-best-practices/actions/workflows/release.yml/badge.svg)

---
Author : Faramarz Karamizadeh
---
**In Step 4 of the second lab, you will need to go into the repo settings > Actions, scroll to the bottom and check Allow GitHub Actions to create and approve pull requests**

---
## Architecture
 
This repository manages shared infrastructure resources:
- **S3 Bucket** — Versioned artifact storage with encryption and lifecycle policies
- **DynamoDB Table** — Application state store with point-in-time recovery
 
## CI/CD Workflows
 
| Workflow | Trigger | Purpose |
|----------|---------|---------|
| CI Pipeline | PR to `main` | Format, validate, security scan, plan |
| CD Pipeline | Push to `main` | Plan + deploy with manual approval |
| Commit Lint | PR open/edit | Enforce conventional commit titles |
| Release Please | Push to `main` | Automated versioning and changelog |
 
## Quick Start
 
```bash
cd terraform
terraform init
terraform plan
terraform apply
```

---
## Requirements

| Name | Version |
| ---- | ------- |
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.6.0 |
| <a name="requirement_aws"></a> [aws](#requirement\_aws) | ~> 5.0 |
| <a name="requirement_random"></a> [random](#requirement\_random) | ~> 3.6 |

## Providers

| Name | Version |
| ---- | ------- |
| <a name="provider_aws"></a> [aws](#provider\_aws) | ~> 5.0 |
| <a name="provider_random"></a> [random](#provider\_random) | ~> 3.6 |

## Modules

No modules.

## Resources

| Name | Type |
| ---- | ---- |
| [aws_dynamodb_table.app_state](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/dynamodb_table) | resource |
| [aws_s3_bucket.artifacts](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket) | resource |
| [aws_s3_bucket_lifecycle_configuration.artifacts](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_lifecycle_configuration) | resource |
| [aws_s3_bucket_public_access_block.artifacts](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_public_access_block) | resource |
| [aws_s3_bucket_server_side_encryption_configuration.artifacts](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_server_side_encryption_configuration) | resource |
| [aws_s3_bucket_versioning.artifacts](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket_versioning) | resource |
| [random_id.suffix](https://registry.terraform.io/providers/hashicorp/random/latest/docs/resources/id) | resource |

## Inputs

| Name | Description | Type | Default | Required |
| ---- | ----------- | ---- | ------- | :------: |
| <a name="input_aws_region"></a> [aws\_region](#input\_aws\_region) | AWS region for all resources | `string` | `"us-east-1"` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Deployment environment | `string` | `"dev"` | no |
| <a name="input_project_name"></a> [project\_name](#input\_project\_name) | Project name used in resource naming | `string` | `"cicd-best-practices"` | no |
| <a name="input_team_name"></a> [team\_name](#input\_team\_name) | Team that owns these resources | `string` | `"platform"` | no |

## Outputs

| Name | Description |
| ---- | ----------- |
| <a name="output_dynamodb_table_arn"></a> [dynamodb\_table\_arn](#output\_dynamodb\_table\_arn) | Application state DynamoDB table ARN |
| <a name="output_dynamodb_table_name"></a> [dynamodb\_table\_name](#output\_dynamodb\_table\_name) | Application state DynamoDB table name |
| <a name="output_s3_bucket_arn"></a> [s3\_bucket\_arn](#output\_s3\_bucket\_arn) | Artifacts S3 bucket ARN |
| <a name="output_s3_bucket_name"></a> [s3\_bucket\_name](#output\_s3\_bucket\_name) | Artifacts S3 bucket name |
