## Setup AWS Environment

1. Go to AWS Management Console
2. Search for Elastic Beanstalk in "Find Services"
3. Click the "Create Application" button
4. Enter "docker" for the Application Name
5. Scroll down to "Platform" and select "Docker" from the dropdown list.
6. Change "Platform Branch" to Docker running on 64bit Amazon Linux 2
7. Click "Create Application"
8. You should see a green checkmark after some time.
9. Click the link above the checkmark for your application. This should open the application in your browser and display a Congratulations message.

### Change from Micro to Small instance type:

Note that a t2.small is outside of the free tier. t2 micro has been known to timeout and fail during the build process on the old platform. However, this may not be an issue on the new Docker running on 64bit Amazon Linux 2 platform. So, these steps may no longer be necessary.

1. In the left sidebar under Docker-env click "Configuration"
2. Find "Capacity" and click "Edit"
3. Scroll down to find the "Instance Type" and change from t2.micro to t2.small
4. Click "Apply"
5. The message might say "No Data" or "Severe" in Health Overview before changing to "Ok"

## Create an IAM User

1. Search for the "IAM Security, Identity & Compliance Service"
2. Click "Create Individual IAM Users" and click "Manage Users"
3. Click "Add User"
4. Enter any name you’d like in the "User Name" field e.g. ebs-user
5. Click "Next"
6. Click "Attach Policies Directly"
7. Search for "beanstalk"
8. Tick the box next to "AdministratorAccess-AWSElasticBeanstalk"
9. Click "Next"
10. Click "Create user"
11. Select the IAM user that was just created from the list of users
12. Click "Security Credentials"
13. Scroll down to find "Access Keys"
14. Click "Create access key"
15. Select "Command Line Interface (CLI)"
16. Scroll down and tick the "I understand..." check box and click "Next"
    Copy and/or download the Access Key ID and Secret Access Key to use in Github Actions.

## Update environment details in deployment file

Change your application_name, environment_name, existing_bucket_name, region and branch name to the values used by your AWS EBS environment inside deploy.yaml:

1. Search for S3 and select buckets, copy the buck name created with application e.g. elasticbeanstalk-us-east-1-123456678
2. Search for EBS and find application name and environment name

## Add secrets to Github repository

1. Navigate to your Github repository.
2. Click Settings
3. Click Secrets
4. Click Actions
5. Click New repository secret
6. Create key/value pair secrets for AWS_ACCESS_KEY, AWS_SECRET_KEY, DOCKER_USERNAME, DOCKER_PASSWORD.

## Deploying App

1. Make a small change to your project files and push to master branch via PR or directly.
2. Go to your Github repository, the click actions and check the status of your build.
3. The status should eventually return with a green checkmark and show "build passing"
4. Go to your AWS Elasticbeanstalk application
5. It should say "Elastic Beanstalk is updating your environment"
6. It should eventually show a green checkmark under "Health". You will now be able to access your application at the external URL provided under the environment name.

## References

1. https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/learn/lecture/11437124#questions/16131052
2. https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/learn/lecture/32547922#questions/17673926
3. https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/learn/lecture/20676694#questions
4. https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/learn/lecture/27975358
