```markdown
# Contributing Guide

## Commit Conventions

This repository uses [Conventional Commits](https://www.conventionalcommits.org/). All PR titles **must** follow this format:

### Allowed Types

| Type | When to Use | Example |
|------|------------|---------|
| `feat` | New infrastructure resource | `feat: add CloudWatch alarm for DynamoDB` |
| `fix` | Bug fix or misconfiguration | `fix: correct S3 bucket policy permissions` |
| `docs` | Documentation only | `docs: update architecture diagram` |
| `chore` | Maintenance, dependencies | `chore: update Terraform provider to 5.30` |
| `refactor` | Code restructuring, no behavior change | `refactor: extract S3 config into module` |
| `ci` | CI/CD workflow changes | `ci: add tfsec to pull request checks` |
| `test` | Adding or updating tests | `test: add validation for DynamoDB schema` |

## Pull Request Process

1. Create a feature branch from `main`: `git checkout -b feat/your-feature`
2. Make changes and commit with conventional messages
3. Push and open a PR with a conventional title
4. CI pipeline runs automatically — all checks must pass
5. Get at least one approval from a reviewer
6. Squash merge to `main`
7. CD pipeline runs and waits for production approval

## CI Pipeline Checks

Every PR must pass these checks before merge:

- **Terraform Format** — `terraform fmt -check`
- **Terraform Validate** — `terraform validate`
- **Security Scan** — tfsec checks for misconfigurations
- **Terraform Plan** — plan output posted as PR comment

## Deployment

Merges to `main` trigger the CD pipeline:
1. Automatic `terraform plan`
2. **Manual approval required** in the `production` environment
3. `terraform apply` executes after approval

## Security

- Never commit `.tfvars` files with real values
- Use GitHub Secrets for AWS credentials
- All S3 buckets must have encryption and public access blocks
- DynamoDB tables must enable encryption and point-in-time recovery


