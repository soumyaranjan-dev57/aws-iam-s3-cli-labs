# AWS IAM, S3 & CLI — Hands-on Labs

A hands-on AWS learning project documenting Identity and Access Management (IAM), Amazon S3 operations, and AWS CLI configuration and troubleshooting.

## Project Overview

This repository documents practical exercises completed while learning core AWS cloud services. It includes step-by-step notes, CLI commands, troubleshooting observations, and screenshots of verified results.

## AWS Services & Tools

- **AWS IAM** — users, permissions, roles, and access management
- **Amazon S3** — bucket and object listing, downloading, editing, and uploading files
- **AWS CLI** — command-line interaction with AWS services
- **Amazon EC2 / Ubuntu** — environment used for AWS CLI practice
- **Python / Shell tools** — supporting tools where applicable

## Hands-on Work

### 1. IAM — Identity and Access Management

- Created and explored an IAM user.
- Reviewed permissions and attached policies for AWS service access.
- Created an IAM role for an AWS service.
- Explored access credentials and MFA settings.

### 2. AWS CLI Setup

- Installed AWS CLI v2 on an Ubuntu EC2 environment.
- Checked the CLI installation and version.
- Configured CLI authentication for practice.
- Troubleshot an S3 permission error.

### 3. Amazon S3 Operations

- Listed S3 buckets using the AWS CLI.
- Listed objects in an S3 bucket.
- Downloaded an HTML file from S3.
- Edited the downloaded file.
- Uploaded the updated file back to S3.
- Verified the updated website in a browser.

## Example Commands

List buckets:

```bash
aws s3 ls
```

List objects in a bucket:

```bash
aws s3 ls s3://YOUR-BUCKET-NAME/
```

Download an object:

```bash
aws s3 cp s3://YOUR-BUCKET-NAME/index.html ./index.html
```

Upload an updated object:

```bash
aws s3 cp ./index.html s3://YOUR-BUCKET-NAME/index.html
```

Replace `YOUR-BUCKET-NAME` with your own bucket name. These commands require appropriate AWS credentials and permissions.

## Repository Structure

```text
aws-iam-s3-cli-labs/
├── README.md
├── docs/
│   └── iam-s3-cli-notes.md
├── commands/
│   └── s3-cli-examples.md
└── screenshots/
    └── practical-results/
```

## Key Learning Outcomes

- Understanding IAM users, roles, and permissions.
- Using AWS CLI to interact with S3.
- Diagnosing and resolving an AWS permissions error.
- Performing S3 object download, update, and upload operations.
- Verifying cloud changes through the browser.

## Security Practices

- Never commit AWS access keys, secret keys, passwords, or credential files.
- Use placeholders instead of account-specific values in public examples.
- Review screenshots and remove sensitive account information before publishing.
- Prefer IAM roles and least-privilege permissions where applicable.

## Notes

This repository is a practical learning record. The documentation reflects the exercises described here; additional files and screenshots will be added after they have been reviewed.

## Author

**Soumya Ranjan Barik**

GitHub: [@soumyaranjan-dev57](https://github.com/soumyaranjan-dev57)
