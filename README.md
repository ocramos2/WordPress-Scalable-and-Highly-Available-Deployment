# Scalable and Highly-Available WordPress Deployment

## Overview

This guide offers steps to deploy a highly available WordPress website on Elastic Beanstalk, integrating an Amazon RDS for robust performance.

## Prerequisites
1. Sign up for an AWS account if you don't have one already. You can do this by visiting the AWS homepage and clicking on the "Create an AWS Account" button.
2. Install the AWS CLI (Command Line Interface) on your local machine. This will allow you to interact with AWS services from your command line. You can find instructions on how to do this in the [AWS CLI User Guide](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html).
3. Install Git on your local machine. This will allow you to clone the necessary WordPress files from the official WordPress GitHub repository.

## Step 1: Launch a DB instance in Amazon RDS
1. Open the Amazon RDS console in your web browser.
2. In the navigation pane, choose "Databases".
3. Choose "Create database".
4. Choose "Standard Create".
5. Under "Engine options", select "MySQL".
6. Under "Templates", select "Free tier".
7. Under "Settings", provide a DB instance identifier, master username, and master password.
8. Under "DB instance size", select "Burstable classes (includes t classes)" and then select "db.t2.micro". This is free-tier eligible.
9. Under "Multi-AZ deployment", select "Do not create a standby instance".
10. Leave the rest of the settings as their defaults and click "Create database".

## Step 2: Download WordPress
1. Open your command line terminal.
2. Navigate to the directory where you want to download WordPress.
3. Run the following command to download WordPress:
```
$ curl https://wordpress.org/latest.tar.gz -o wordpress.tar.gz
```
4. Extract the downloaded file with this command:
```
$ tar -xvf wordpress.tar.gz
```

## Step 3: Launch an Elastic Beanstalk environment
1. Open the Elastic Beanstalk console in your web browser.
2. Click on "Create a new environment".
3. Select "Web server environment" and click "Select".
4. Under "Platform", select PHP.
5. Under "Application code", select "Sample application".
6. Click on "Create environment".

## Step 4: Configure security groups and environment properties
1. Once your environment is created, click on its name in the Elastic Beanstalk console.
2. In the navigation pane, choose "Configuration".
3. In the "Instances" configuration category, click on "Edit".
4. Under "EC2 security groups", choose the security group that's associated with your RDS instance.
5. Click on "Apply".

## Step 5: Configure and deploy your application
1. In your local WordPress directory, open `wp-config.php` in a text editor.
2. Replace `database_name_here`, `username_here`, and `password_here` with your RDS database name, username, and password respectively.
3. Save and close `wp-config.php`.
4. In your command line terminal, navigate to your WordPress directory.
5. Run the following command to create a .zip file of your WordPress directory:
```
$ zip ../wordpress.zip -r *
```
6. In the Elastic Beanstalk console, navigate to your environment.
7. Click on "Upload and Deploy".
8. Click on "Choose File" and select the .zip file you just created.
9. Click on "Deploy".

## Step 6: Install WordPress
1. Once your application has been deployed, click on the URL next to your environment name in the Elastic Beanstalk console.
2. You should now see the WordPress installation wizard in your web browser.
3. Follow the prompts to install WordPress.

## Step 7: Update keys and salts
1. In the Elastic Beanstalk console, navigate to your environment.
2. In the navigation pane, choose "Configuration".
3. Under "Software", choose "Edit".
4. For "Environment properties", modify the following properties:
   - `AUTH_KEY`
   - `SECURE_AUTH_KEY`
   - `LOGGED_IN_KEY`
   - `NONCE_KEY`
   - `AUTH_SALT`
   - `SECURE_AUTH_SALT`
   - `LOGGED_IN_SALT`
   - `NONCE_SALT`
5. Click on "Apply".

## Step 8: Remove access restrictions
1. In your local WordPress directory, delete the `.ebextensions/loadbalancer-sg.config` file.
2. Create a new .zip file of your WordPress directory.
3. In the Elastic Beanstalk console, navigate to your environment.
4. Click on "Upload and Deploy".
5. Click on "Choose File" and select the new .zip file you just created.
6. Click on "Deploy".

## Step 9: Configure your Auto Scaling group
1. In the Elastic Beanstalk console, navigate to your environment.
2. In the navigation pane, choose "Configuration".
3. In the "Capacity" configuration category, choose "Edit".
4. In the "Auto Scaling group" section, set "Min instances" to 2.
5. Click on "Apply".

## Step 10: Upgrade WordPress
1. Back up your site and deploy it to a new environment.
2. Download the new version of WordPress and repeat the steps above to deploy it to Elastic Beanstalk.

## Step 11: Clean up
1. In the Elastic Beanstalk console, navigate to your environment.
2. Choose "Actions", and then choose "Terminate environment".
3. Confirm environment termination.
4. In the Amazon RDS console, navigate to your DB instance.
5. Choose "Actions", and then choose "Delete".
6. Confirm deletion.

## Next Steps
Consider using the Elastic Beanstalk Command Line Interface (EB CLI) for easier management of environments and deployment of your application from the command line.

## Conclusion

In this project, we demonstrated how to deploy a high-availability WordPress website with an external Amazon RDS database to Elastic Beanstalk. By following these steps, you can create a scalable and reliable WordPress website that can handle high levels of traffic.

## Acknowledgment

This tutorial is adapted from the [AWS Elastic Beanstalk tutorial for deploying a high-availability WordPress website](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/php-hawordpress-tutorial.html) provided by Amazon Web Services. We extend our gratitude to AWS for providing this valuable resource, which served as the foundation for the "Scalable and Highly-Available WordPress Deployment" tutorial.
