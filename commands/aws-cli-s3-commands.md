# AWS CLI — S3 Operations

## Overview

This document covers the AWS CLI workflow used to interact with Amazon S3 from an Ubuntu EC2 environment. It includes installation, bucket and object listing, file transfer, and troubleshooting an IAM permission error.

## Environment

| Component | Details |
|---|---|
| Operating system | Ubuntu on Amazon EC2 |
| CLI | AWS CLI v2 |
| Verified CLI version | `2.38.6` |
| AWS Region used for the project | `ap-south-1` |

## 1. Install AWS CLI

Install the required utilities:

```bash
sudo apt update
sudo apt install -y curl unzip
```

Download and extract the AWS CLI v2 installer:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
```

Install and verify:

```bash
sudo ./aws/install
aws --version
```

**Observed version:** `aws-cli/2.38.6`

## 2. Configure Credentials Securely

Configure credentials locally using an authorized IAM identity:

```bash
aws configure
```

Enter credentials only in the local terminal's interactive prompts. Do not place access keys in source files, screenshots, command examples, or Git commits.

For this repository, use placeholders in any examples and never upload `~/.aws/credentials`.

## 3. List S3 Buckets

```bash
aws s3 ls
```

This command initially returned `AccessDenied` because the IAM identity lacked the `s3:ListAllMyBuckets` permission.

After the S3 permissions were updated, the command successfully listed the available buckets.

## 4. List Objects in the Website Bucket

```bash
aws s3 ls s3://YOUR-BUCKET-NAME/
```

Replace `YOUR-BUCKET-NAME` with the intended bucket name.

The website bucket contained `index.html` and `error.html`.

## 5. Download the Website File

```bash
aws s3 cp s3://YOUR-BUCKET-NAME/index.html ./index.html
```

This downloads the S3 object into the current local directory.

## 6. Edit and Upload the File

Edit the downloaded HTML file:

```bash
vim index.html
```

The page title was updated locally.

Upload the modified file:

```bash
aws s3 cp ./index.html s3://YOUR-BUCKET-NAME/index.html
```

Verify the object listing:

```bash
aws s3 ls s3://YOUR-BUCKET-NAME/
```

The updated object appeared in the listing, and the change was verified in the browser.

## Troubleshooting: `AccessDenied`

**Observed issue:** `aws s3 ls` failed with an authorization error related to `s3:ListAllMyBuckets`.

**Cause:** The configured IAM identity did not have the permission required to list all general-purpose S3 buckets.

**Resolution performed:** `AmazonS3FullAccess` was attached to the IAM user, after which the command succeeded.

**Security consideration:** `AmazonS3FullAccess` is broad. A production implementation should grant only the specific actions and resources required, such as access to a designated bucket and its objects.

## Results

- AWS CLI v2 installed and version verified.
- S3 bucket listing succeeded after permission correction.
- Website objects listed through the CLI.
- `index.html` downloaded, edited, and uploaded.
- Updated website content verified in the browser.

## Security Checklist

- [ ] Confirm exposed access keys have been revoked.
- [ ] Keep AWS credential files out of Git.
- [ ] Redact sensitive information from terminal screenshots.
- [ ] Replace broad IAM permissions with least-privilege access where appropriate.

Only mark security checks complete after verifying them.
