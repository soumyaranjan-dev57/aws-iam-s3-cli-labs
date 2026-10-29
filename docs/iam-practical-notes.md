AWS IAM Practical Notes

1. Objective

Practise AWS Identity and Access Management (IAM), create a user, explore permission policies, create an EC2-trusted role, and troubleshoot an S3 access-permission issue.

2. IAM User Creation

Console path: AWS Console → IAM → Users → Create user

Steps performed:

Opened IAM in the AWS Console.

Created an IAM user named soumya.

Enabled console access.

Selected an automatically generated password and required a password reset at first sign-in.

Signed in and reset the password successfully.

Security: Never commit passwords, credential CSV files, account IDs, or sign-in URLs to this repository.

3. Permission Policies

The initial user policy selection included:

AmazonEC2FullAccess

AmazonS3ExpressFullAccess

IAMFullAccess

IAMUserChangePassword

Later, AmazonS3FullAccess was attached to resolve an S3 bucket-listing permission error.

Important learning

AmazonS3ExpressFullAccess did not provide the permission needed for the normal S3 bucket-listing command used in this exercise.

Attaching AmazonS3FullAccess resolved the observed AccessDenied error.

Security improvement: These are broad permissions. For real workloads, review the required actions and resources and use least-privilege policies instead.

4. IAM Role Creation

Console path: IAM → Roles → Create role

Steps performed:

Selected AWS service as the trusted entity.

Selected EC2 as the use case.

Selected the AmazonRDSFullAccess permission policy.

Created a role named ec2-to-rds-role.

Verification status

Role creation: completed.

Attachment of the role to an EC2 instance: not confirmed.

Successful RDS connectivity: not confirmed.

Creating a role alone does not prove that an EC2 instance is using it or that database connectivity works.

5. Identity Providers and MFA

Explored the Identity Providers section.

Attempted MFA setup using an authenticator application.

The later console status showed no MFA devices.

Therefore, MFA is not recorded as successfully configured in this practical.

6. S3 Permission Troubleshooting

Problem

Running the following command initially returned AccessDenied:

aws s3 ls

The error indicated that the identity lacked s3:ListAllMyBuckets.

Fix performed

AWS Console → IAM → Users → soumya → Permissions → Add permissions → Attach policies directly → AmazonS3FullAccess.

The bucket-listing command subsequently succeeded.

Lesson learned

AWS CLI commands run with the permissions of the configured AWS identity. A successful CLI installation does not automatically grant access to AWS resources.

7. Security Checklist

Verify that exposed access keys have been deactivated or deleted.

Ensure credentials and credential CSV files are not committed.

Inspect screenshots and redact sensitive account information.

Verify whether the EC2 role is attached.

Configure and verify MFA.

Replace broad permissions with least-privilege policies where practical.

Only mark an item complete after verifying it in the AWS Console.
