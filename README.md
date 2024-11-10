# AWS Static Website Hosting Project

## Project Overview
This project demonstrates how to host a static website using AWS S3, with optional integration of CloudFront for performance and Route53 for domain management.

## Technologies Used
- **AWS S3** for static file storage
- **Amazon CloudFront** for content distribution (optional)
- **Route 53** for DNS management (optional)

## Understanding the Technologies Used
- **AWS S3**: An AWS S3 bucket is a storage container provided by Amazon Web Services (AWS) within its Simple Storage Service (S3). It is used to store and organize data in the cloud. Here’s a breakdown of key aspects of an S3 bucket:
  - **Key Features:**
    - **Object Storage:** S3 buckets store data as objects, which consist of the file itself and associated metadata.
    - **Scalable Storage:** S3 is designed to handle large volumes of data, scaling up or down based on your storage needs.
    - **Data Accessibility:** Objects in an S3 bucket can be accessed through the AWS Management Console, APIs, or command-line tools, allowing for easy integration with other services or applications.
    - **Permissions and Access Control:** You can set fine-grained access controls at both the bucket and object level using bucket policies, user roles, or access control lists (ACLs).
    - **Security:** AWS S3 provides data encryption at rest and in transit, as well as versioning and replication features for added data protection.
    - **Global Availability:** You can choose to create buckets in specific AWS regions to optimize latency, ensure data redundancy, or comply with regional data regulations.

  - **Common Usecases:**
    - **Data Backups:** Storing backups of files, databases, or entire applications.
    - **Static Website Hosting:** Hosting static websites, with files such as HTML, CSS, JavaScript, images, and other media.
    - **Data Lake:** Using buckets as repositories for large-scale data storage for analytics.
    - **File Sharing:** Facilitating the sharing and distribution of files and content across users or applications.

  - **Structure:**
    - **Buckets:** Top-level containers where data is stored.
    - **Objects:** Individual files stored in buckets, identified by a unique key within the bucket.
    - **Folders:** Not actual entities, but used to organize objects by prefixing object keys with a directory-like structure.
      
- **Amazon CloudFront** for content distribution
  - Faster Content Delivery: CloudFront caches content at edge locations around the globe, reducing latency for users.
  - Scalability: Automatically scales to handle spikes in traffic.
  - Security Features: Provides options such as custom SSL/TLS certificates, DDoS protection, and AWS WAF (Web Application Firewall) integration.
  - Compression and Optimization: Serves compressed versions of files for optimized delivery.


## S3 Setup Steps
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
   - Issue faced: Without .index.html accessing the cloudfront URL does seem to work
   - Fix - In the CloudFront distribution settings under defualt root object enter "index.html" - This sixed the issue

## Integrate Amazon CloudFront with an S3 Bucket
1.  Log in to AWS Management Console
   - Go to the CloudFront service.
2. Create a CloudFront Distribution
   - Click on “Create Distribution” and choose “Web” as the distribution type.
   - In the Origin Settings:
     - Origin Domain Name: Select your S3 bucket from the dropdown list. It should look like my-bucket-name.s3.amazonaws.com.
     - Origin Path: Leave this blank unless you want CloudFront to only use a specific path in the bucket.
     - Origin ID: This will be auto-populated, but you can customize it if needed.
     - Restrict Bucket Access: Set this to “Yes” to enhance security by ensuring only CloudFront can access the bucket directly.
     - Origin Access Control: Create or use an existing Origin Access Control (OAC) to allow CloudFront to access your bucket while preventing direct public access.
3. Configure Default Cache Behavior
   - Viewer Protocol Policy: Choose “Redirect HTTP to HTTPS” or “HTTPS Only” for secure access.
   - Cache and Origin Request Settings:
4. Set Distribution Settings
   - Price Class: Choose a price class based on where you want CloudFront to serve content (e.g., “Use Only U.S., Canada, and Europe” for cost savings).
   - Alternate Domain Names (CNAMEs): Enter your custom domain name if you have one (e.g., www.example.com).
5. Review and Create the Distribution
   - Click “Create Distribution”.
   - It may take a few minutes for CloudFront to deploy the distribution. You will see the status change to “Deployed” once it is ready.
6. Update the S3 Bucket Policy
   - Ensure the S3 bucket policy allows access only through CloudFront. Here is a sample policy:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": {
        "Service": "cloudfront.amazonaws.com"
      },
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket-name/*",
      "Condition": {
        "StringEquals": {
          "AWS:SourceArn": "arn:aws:cloudfront::account-id:distribution/distribution-id"
        }
      }
    }
  ]
}
```
   - Replace my-bucket-name, account-id, and distribution-id with your specific values.
7. Test Your Setup
   - Visit your CloudFront domain /index.html (or custom domain if configured) to ensure your static website is loading correctly.
8. Final Note:
   - Make sure to monitor the performance using CloudFront metrics in Amazon CloudWatch and tweak the caching and behavior settings as necessary to optimize performance for your specific use case.

## Use Route 53 for a Custom Domain (Optional)
   - Yet to complete

## Screenshots

![Screenshot 1](https://github.com/user-attachments/assets/5714ec49-5f43-49f7-8696-381626ac51a1)

![Screenshot 2](https://github.com/user-attachments/assets/2ccea6cc-856e-4bbc-aa55-a5ef5f64c44f)

![Screenshot 3](https://github.com/user-attachments/assets/2a00fc8f-85b4-4f6e-9428-687a7ae7607a)


## Live Demo
[Visit the live site here](https://d21elmou5l4ub.cloudfront.net/) 

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
