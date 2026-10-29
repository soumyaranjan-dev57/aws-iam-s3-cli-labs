# AWS IAM, S3 Static Website Hosting & AWS CLI

A hands-on AWS cloud project covering Identity and Access Management (IAM), Amazon S3 static website hosting, AWS CLI installation, permission troubleshooting, and website file updates.

## Project Overview

This project documents practical AWS exercises completed while learning cloud fundamentals. It demonstrates how a static website is hosted on Amazon S3, how IAM permissions affect AWS CLI operations, and how website files can be downloaded, edited, uploaded, and verified.

## AWS Services & Tools

- **AWS IAM** — users, policies, roles, and permissions
- **Amazon S3** — object storage and static website hosting
- **AWS CLI v2** — command-line interaction with AWS
- **Amazon EC2 (Ubuntu)** — environment used for CLI practice
- **HTML & CSS** — portfolio website and custom error page
- **Vim** — editing HTML files on Ubuntu

## Project Workflow

1. Create and configure an S3 bucket.
2. Enable static website hosting.
3. Configure public-read access for website objects.
4. Upload the portfolio website and custom error page.
5. Create an IAM user and explore IAM roles and policies.
6. Install AWS CLI v2 on an Ubuntu EC2 instance.
7. Troubleshoot an S3 `AccessDenied` error.
8. List S3 buckets and objects using AWS CLI.
9. Download, edit, and upload `index.html`.
10. Verify the updated website in a browser.

## 1. Amazon S3 Static Website Hosting

**AWS Region:** Asia Pacific (Mumbai) — `ap-south-1`

**Website files:**

| File | Purpose |
|---|---|
| `index.html` | Main SRB DevOps & Cloud portfolio page |
| `error.html` | Custom cyberpunk-style 404 error page |

### Configuration

- Created the S3 bucket.
- Enabled static website hosting.
- Set `index.html` as the index document.
- Prepared and uploaded `error.html` as the custom error page.
- Configured a bucket policy to allow public reads of website objects.

**Website endpoint:**  
`http://YOUR-BUCKET-WEBSITE-ENDPOINT`

Replace the placeholder with the website endpoint from your S3 bucket's Properties page.

### Bucket Policy

The following is the policy pattern used for public read access to website objects. Replace the bucket placeholder before using it.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "GetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
    }
  ]
}
```

**Security note:** This policy can make objects publicly readable when the relevant S3 and account settings permit it. Never store confidential files in a public website bucket.

## 2. IAM — Identity and Access Management

Practical exercises included:

- Creating an IAM user with console access.
- Reviewing attached permission policies.
- Testing access to AWS services.
- Creating an EC2-trusted IAM role with an RDS-related policy.
- Exploring the Identity Providers section.
- Attempting to configure multi-factor authentication (MFA).
- Creating an access key for CLI practice.

### Permission Troubleshooting

The first `aws s3 ls` attempt returned `AccessDenied` because the IAM identity did not have the required `s3:ListAllMyBuckets` permission.

Attaching `AmazonS3FullAccess` allowed the S3 listing command to succeed.

**Learning:** AWS CLI access depends on the permissions of the identity being used. Broad permissions should be replaced with least-privilege permissions wherever possible.

Some IAM verification tasks remain separate and should not be considered complete until confirmed.

## 3. AWS CLI Installation on Ubuntu EC2

Checked whether AWS CLI was installed:

```bash
aws
```

The command was initially unavailable.

Installed the required packages:

```bash
sudo apt update
sudo apt install -y curl unzip
```

Downloaded the AWS CLI v2 installer:

```bash
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
```

Extracted the installer:

```bash
unzip awscliv2.zip
```

Installed AWS CLI:

```bash
sudo ./aws/install
```

Verified the installation:

```bash
aws --version
```

**Observed version:** AWS CLI `2.38.6`

## 4. AWS CLI — Amazon S3 Operations

### List S3 buckets

```bash
aws s3 ls
```

After fixing the permissions issue, the command listed the available buckets.

### List bucket objects

```bash
aws s3 ls s3://YOUR-BUCKET-NAME/
```

The website bucket contained:

- `index.html`
- `error.html`

### Download `index.html`

```bash
aws s3 cp s3://YOUR-BUCKET-NAME/index.html ./index.html
```

### Edit the HTML file

```bash
vim index.html
```

The page title was updated by adding `!` after `SRB`.

### Upload the updated file

```bash
aws s3 cp ./index.html s3://YOUR-BUCKET-NAME/index.html
```

### Verify the upload

```bash
aws s3 ls s3://YOUR-BUCKET-NAME/
```

The updated `index.html` appeared in the bucket listing.

**Result:** The download → local edit → upload → browser verification workflow was completed successfully.

## 5. Verification Status

- S3 bucket created and configured for static website hosting.
- `index.html` uploaded and website opened in a browser.
- Custom `error.html` prepared and uploaded.
- AWS CLI v2 installed and version verified on Ubuntu EC2.
- S3 permission error diagnosed and resolved for the listing task.
- HTML file downloaded, edited, uploaded, and verified in the browser.
- Custom error-page behavior for a nonexistent URL requires separate verification.
- IAM role attachment, MFA status, and credential cleanup must be verified separately.

## 6. Repository Structure

```text
aws-iam-s3-cli-labs/
├── README.md
├── docs/
│   ├── iam-practical-notes.md
│   └── s3-static-website-notes.md
├── commands/
│   └── aws-cli-s3-commands.md
└── screenshots/
    ├── iam/
    ├── s3-static-website/
    └── aws-cli/
```

## 7. Security Practices

- Never publish AWS access keys, secret keys, passwords, credential CSV files, or local AWS credential files.
- Redact account identifiers and sign-in URLs from public screenshots and documentation.
- Use placeholders in reusable commands and policy examples.
- Review public bucket policies carefully.
- Prefer IAM roles and least-privilege permissions.
- Verify that exposed credentials have been revoked before publishing related screenshots or notes.

## Key Learning Outcomes

- Understanding IAM users, roles, and permission policies.
- Hosting a static website using Amazon S3.
- Working with website index and error documents.
- Installing and verifying AWS CLI v2.
- Troubleshooting an AWS permissions error.
- Performing S3 object download, edit, upload, and verification operations.

## Author

**Soumya Ranjan Barik**  
GitHub: [@soumyaranjan-dev57](https://github.com/soumyaranjan-dev57)

*This repository documents hands-on AWS learning. Practical results and pending verification items are stated separately to keep the documentation accurate.*
