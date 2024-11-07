# AWS Static Website Hosting Project

## Project Overview
This project demonstrates how to host a static website using AWS S3, with optional integration of CloudFront for performance and Route53 for domain management.

## Technologies Used
- **AWS S3** for static file storage
- **Amazon CloudFront** for content distribution (optional)
- **Route 53** for DNS management (optional)

## Setup Steps
1. Create and configure an S3 bucket for static website hosting.
2. Upload website files.
3. Configure permissions for public access.
4. (Optional) Integrate with CloudFront and Route 53.

## Screenshots
![Website Screenshot](https://private-user-images.githubusercontent.com/47561553/383953747-442d3c01-977f-4e94-accc-a6741065f14b.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzA5ODIzMzYsIm5iZiI6MTczMDk4MjAzNiwicGF0aCI6Ii80NzU2MTU1My8zODM5NTM3NDctNDQyZDNjMDEtOTc3Zi00ZTk0LWFjY2MtYTY3NDEwNjVmMTRiLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMDclMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTA3VDEyMjAzNlomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTQyYzlmOTBiYjY2MzBmOWMzZWMwZGExZGM1OGYzYjliNGNiYTM0OThhZWFlMzFjYTEwOTljYTEwYjgyNzQwYzcmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.Ju9v3XZEKww2JAGkYsFgb6dj_R4B8KmqdK56_eMaItc)

![Website Screenshot](https://private-user-images.githubusercontent.com/47561553/383953735-169ce5c7-60bc-495e-922a-b81d9271e166.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzA5ODIzNDQsIm5iZiI6MTczMDk4MjA0NCwicGF0aCI6Ii80NzU2MTU1My8zODM5NTM3MzUtMTY5Y2U1YzctNjBiYy00OTVlLTkyMmEtYjgxZDkyNzFlMTY2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMDclMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTA3VDEyMjA0NFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWQ0ODUxNGU3ZGY5ZDkzODU5OWFkOGU4YTYzYjgzNTYxNTM2Nzg2MjYwMzNkMGY5NmU4YThhMTE2Zjg2NDc2NmQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.h59n2CdbYiYy9xu1tjcNf16g2cJo-mSgl9INo0jSHKE)

![Website Screenshot](https://private-user-images.githubusercontent.com/47561553/383953743-1b2f3412-b5c0-4b79-91af-766804ecdec8.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzA5ODIzNDQsIm5iZiI6MTczMDk4MjA0NCwicGF0aCI6Ii80NzU2MTU1My8zODM5NTM3NDMtMWIyZjM0MTItYjVjMC00Yjc5LTkxYWYtNzY2ODA0ZWNkZWM4LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMDclMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTA3VDEyMjA0NFomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTM0ZDUwNjBkYjRkMTZlOGFmY2U5ZDZjNDcxNDIyOGE1ZmFkNjYyMGJhZjQ3ZWE3ZWJkZjk0ZmZiYzkwMjQ1MzgmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.4S0V54R7R4ki7wVaLykOVH2j3sDSJdYM3lIhQM_760A)

## Live Demo
[Visit the live site here](http://my-website211.com.s3-website-us-east-1.amazonaws.com/) 

## Author
[Harish Sundaram](https://github.com/harishsun)

## Important Pre-requisite

You do not need to use the root account for setting up and managing an S3 bucket or any other AWS service as part of your project. In fact, it is best practice to avoid using the root account for day-to-day tasks or any operations beyond initial account setup and billing management.

Why Avoid the Root Account?
The root account has unrestricted access to all AWS resources and services, which makes it highly powerful but also highly vulnerable. If compromised, it could lead to serious security issues. Instead, you should create and use IAM (Identity and Access Management) users with the necessary permissions for managing AWS resources.

### Setting Up an IAM User for AWS Project Work
1. Log in to the AWS Management Console with your root account to create an IAM user.
2. Navigate to the IAM service.
3. Click on “Users” and then “Add users”.
4. Enter a user name (e.g., aws-admin or project-user).
5. Select “Programmatic access” and/or “AWS Management Console access”, depending on how you want to use the account.
6. Attach permissions:
 - Use an existing policy like AdministratorAccess (only if you need full access) or create a custom policy that limits permissions to only the services you need (e.g., AmazonS3FullAccess, CloudFrontFullAccess).
7. Review and create the user. Make sure to download the access key ID and secret access key if you choose programmatic access.
### Using the IAM User Account
 - Sign in to the AWS Management Console using the IAM user credentials.
 - Use the AWS Command Line Interface (CLI) or Software Development Kits (SDKs) with the access key ID and secret access key if needed.
### Best Practices
 - Grant the least privilege necessary for the tasks you are performing.
 - Enable MFA (Multi-Factor Authentication) for the IAM user to enhance security.
 - Use IAM roles instead of users where appropriate, especially if deploying services or applications within AWS that need permissions.
### Final Note
 - Always keep your root account credentials secure and use them only when absolutely necessary (e.g., account recovery or billing). Using an IAM user or role for daily AWS operations ensures better security practices and minimizes potential risks.
