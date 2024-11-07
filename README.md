# AWS Static Website Hosting Project

## Project Overview
This project demonstrates how to host a static website using AWS S3, with optional integration of CloudFront for performance and Route53 for domain management.

## Technologies Used
- **AWS S3** for static file storage
- **Amazon CloudFront** for content distribution (optional)
- **Route 53** for DNS management (optional)

## Setup Steps
1. Create and configure an S3 bucket for static website hosting
   - Log in to the AWS Management Console and navigate to the S3 service.
   - Create a new bucket by clicking the “Create bucket” button.
      - Name the bucket: Ensure the bucket name matches the website domain (e.g., my-website.com), as this will simplify future configurations if you plan to use a custom domain.
      - Choose a region: Select a region close to your target audience for lower latency.
   - Configure bucket settings:
      - Leave Block Public Access enabled initially. This will be configured later for public access.
 
2. Upload website files
   - Prepare your website files: Ensure you have the static files ready (e.g., index.html, styles.css, scripts.js). [**Note:** Use your own files or download samples from online. I downloaded them from https://www.free-css.com/free-css-templates]
   - Upload files to the bucket:
     - Open the bucket and click “Upload”.
     - Drag and drop your website files or use the file browser to select them.
     - Click “Upload” to complete the process.

4. Configure Bucket for static website hosting
   - Navigate to “Properties” for your bucket.
   - Scroll down to the “Static website hosting” section and enable it.
     - Select “Use this bucket to host a website”.
     - Specify the “index document” (e.g., index.html). [**Note:** Make sure this document is not inside the folder, when u upload the first set of file make sure you upload them as files and not folders and then on for the subfolder use folder option]
     - If needed, specify an “error document” (e.g., error.html).
   - Save the configuration.
 
5. Set Bucket Permissions for Public Access
   - Navigate to the “Permissions” tab of the bucket.
   - Edit the Bucket policy:
     - Add a policy that allows public read access to the objects in the bucket. Use the following json policy template:
     - Replace my-website.com with your bucket name.
  ```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-website.com/*"
    }
  ]
}
```


  - Save the policy and ensure Block Public Access settings are turned off as needed.
      
     
6. Test Your Static Website
   - Copy the “Bucket website endpoint” provided in the static website hosting configuration.
   - Paste it into your browser to access your newly hosted site.
   - Verify that the content loads correctly.

7. Integrate Amazon CloudFront for Performance (Optional)
   - Yet to complete
8. Use Route 53 for a Custom Domain (Optional)
   - Yet to complete

## Screenshots
![Website Screenshot1](https://private-user-images.githubusercontent.com/47561553/383953747-442d3c01-977f-4e94-accc-a6741065f14b.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzA5ODc5NTcsIm5iZiI6MTczMDk4NzY1NywicGF0aCI6Ii80NzU2MTU1My8zODM5NTM3NDctNDQyZDNjMDEtOTc3Zi00ZTk0LWFjY2MtYTY3NDEwNjVmMTRiLnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMDclMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTA3VDEzNTQxN1omWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPWVlYmZhNjdjYzQ3MTY1YmMyNmI1YmI5ZTg3ZmFlYjI3MGY4ZjZiNDJmNDI2ZmYwYzIxZTMyYmUzZjFlNzRlOTAmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.B42YdTvGLylSUI9H0akTwYJwgd3O3h2UD1s_kg2pJQ8)

![Website Screenshot2](https://private-user-images.githubusercontent.com/47561553/383953735-169ce5c7-60bc-495e-922a-b81d9271e166.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzA5ODgxNDksIm5iZiI6MTczMDk4Nzg0OSwicGF0aCI6Ii80NzU2MTU1My8zODM5NTM3MzUtMTY5Y2U1YzctNjBiYy00OTVlLTkyMmEtYjgxZDkyNzFlMTY2LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMDclMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTA3VDEzNTcyOVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTRiZjM4ZDVkNzVmYTc2NDgxMDk5ZmRmODlkOTAyOTk2ZmU0NWMwNjczNTY2ZTcyYzgxODczNjljMmNlZDcwODQmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.qmaYIGkpCHcBZNyKZ-O7U9X7PIsJJkP6NhNFrd9JmrE)

![Website Screenshot3](https://private-user-images.githubusercontent.com/47561553/383953743-1b2f3412-b5c0-4b79-91af-766804ecdec8.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3MzA5ODgxNDksIm5iZiI6MTczMDk4Nzg0OSwicGF0aCI6Ii80NzU2MTU1My8zODM5NTM3NDMtMWIyZjM0MTItYjVjMC00Yjc5LTkxYWYtNzY2ODA0ZWNkZWM4LnBuZz9YLUFtei1BbGdvcml0aG09QVdTNC1ITUFDLVNIQTI1NiZYLUFtei1DcmVkZW50aWFsPUFLSUFWQ09EWUxTQTUzUFFLNFpBJTJGMjAyNDExMDclMkZ1cy1lYXN0LTElMkZzMyUyRmF3czRfcmVxdWVzdCZYLUFtei1EYXRlPTIwMjQxMTA3VDEzNTcyOVomWC1BbXotRXhwaXJlcz0zMDAmWC1BbXotU2lnbmF0dXJlPTEwNzY4YTM1ZDk5YTI4MjYzZTQxNjQyYTJiYzE0NDIwYTVlYTllMWVkZmZhNmZjODVkODk5OTcwNDVlMzk2YTYmWC1BbXotU2lnbmVkSGVhZGVycz1ob3N0In0.27CYGlmRNjYAZzQSyDguaf61_5nECQ4W21YldDXjQhM)

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
