# s3_static_site
Static web site content with github action to publish to S3

# Prerequisites

- Have an AWS account and created an S3 bucket setup to host a static website.  See [https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html](https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html)
- The github repo with the static website source files should be public to allow Github actions to work

# Set AWS Credentials

## Setup in AWS

Create a new IAM user group and user specifically for publishing the static site and with limited access to S3

- In AWS console, click your username in the top menu and select Security Credentials (Or just go to the IAM view)
- Click User Groups, then Create Group
- Provide a group name, like "static_site_publisher"
- In the filter, type "s3" and select "AmazonS3FullAccess" policy.  Click "Create Group" button
- Create a user for the new group.  Click on the Users side menu button and then "Add User"
- Provide a user name, like "static_site_publisher", and click Next.
- Select the newly created group and click Next.
- On the Review and Create screen, just click "Create User"
- From the Users view, click on the new user.  In the Summary section, click on "Create Access Key" (also found on Security Credentials tab), select "Other" for the use case, then click Next.
- Add a description for the key if you want, then click "Create Access Key"
- Copy the Access Key and Secret Access Key to a scratchpad temporarily

# Add credentials to Github Repo

Add the credentials as repository secrets so that github actions can use them to access AWS S3

- Go to the github repo Settings -> Security -> Secrets and Variables -> Actions
- Create two new Repository secrets
    - Create a new secret called "AWS_ACCESS_KEY_ID" and paste the access key id value 
    - Create a new secret called "AWS_SECRET_ACCESS_KEY" and paste the access key secret value

# Create your static website in the repo's "public folder"

- Whatever is in the public folder is what will be synced to S3

# Configure the s3_publish_site.yml file

- Update the .github\workflows\s3_publish_site.yml file to publish to your S3 bucket by modifying it to your S3 bucket name
