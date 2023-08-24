# AWS: Cloud Servers & Elastic Beanstalk

Putting to work the ability to upload an api to the cloud in multiple ways.

* I used my City Explorer API in these instances.

## Links

EB-GUI = http://aws-test-app-env.eba-hwmcvmm7.us-west-2.elasticbeanstalk.com/

EB-CLI = 

## 1: Creating an application with the Elastic Beanstalk GUI

Use "Elastic Beanstalk" to Deploy a NodeJS server to an EC2 instance at AWS.

This requires 2 parts:

- An "Environment" (container) for our application to run in
- The application code itself to be deployed "into" the environment

Elastic Beanstalk (EB) will automatically wire up essential AWS services to create and deploy a running application.

For Node.js applications, this is generally just going to be an EC2 server instance along with an S3 bucket that stores our files.

Before starting you will need to make sure your code is linked with github & at AWS you will need to go to IAM and create a user.
-give the user a name
-give them permissions (I used 'AdministratorAccess' to grant full permissions i believe)

- Click 'Create application'
- Then web server environment
- Choose NodeJS as your platform
- Upload a .zip file with your application source code
    - Do not include node_modules or package-lock.json
- Use existing service role (rhett)
- Trust default settings for all of the next steps

This will create your application and environment in one step, giving you a full GUI from where you can manage the app

## 2: Creating an application using the command line only

Second way to create a new application with EB. Either way, all of your environments and applications will be available in the AWS Developer Console (GUI) for you to manage.

First, ensure that you've installed the AWS CLI and the aws eb command line utilities.
- Then in the terminal 'aws configure'
- Get our user (unique for each user) access id and secret key to use in configure (saved in phone)
- us-west-2
- json

1. eb init - Initializes your folder as an Elastic Beanstalk application.
    - Choose your region (us-west-2)
    - Choose [Create new Application]
        - Note: If you already have an application, you could also choose that to connect
    - Answer the other questions as appropriate
        - Choose Node.js at the correct version

2. eb create my-environment-name - Create an "environment" for your app to reside in.

3. eb deploy to deploy your new application to your new environment.
    - You'll also use this whenever you make code changes

You can then use some other eb commands to manage your apps.

    - eb open to open your app in the browser
    - eb list to get a list of apps
    - eb ssh to ssh (login) to one of your apps
    - eb health to get a health check on your environments

## BONUS: Auto-Deploy
You can also use GitHub Actions to auto-deploy your source code to your EB Environment whenever you check in your code.

- Browse the GitHub Marketplace for actions you can import into your repo. There are many.
