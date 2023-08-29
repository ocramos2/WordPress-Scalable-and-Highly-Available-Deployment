# Deploying a High-Availability WordPress Website with External Amazon RDS Database

This guide will walk you through the process of deploying a high-availability WordPress website using an external Amazon RDS database with AWS Elastic Beanstalk. The website will also utilize Amazon Elastic File System (Amazon EFS) for shared file storage.

## Prerequisites

- Basic knowledge of AWS services.
- AWS account with permissions to create resources.
- Command line terminal or shell.
- Access to the AWS Elastic Beanstalk console.

## Step 1: Launch an Amazon RDS DB Instance

1. Open the Amazon RDS console.
2. Launch a Multi-AZ MySQL DB instance for high availability.
3. Modify the security group of the DB instance to allow inbound traffic on the appropriate port (e.g., 3306).
4. Take note of the DB instance endpoint and credentials.

## Step 2: Download WordPress and Set Up Project

1. Download WordPress and configuration files:
   ```sh
   $ curl -o wordpress.tar.gz -L https://wordpress.org/latest.tar.gz
   $ wget -O eb-php-wordpress-v1.zip https://github.com/aws-samples/eb-php-wordpress/releases/download/v1.1/eb-php-wordpress-v1.zip
   $ tar -xvf wordpress.tar.gz
   $ mv wordpress wordpress-beanstalk
   $ cd wordpress-beanstalk
   $ unzip ../eb-php-wordpress-v1.zip

   ```

## Step 3: Launch an Elastic Beanstalk Environment

1. Open the Elastic Beanstalk console.
2. Create an Elastic Beanstalk environment using the PHP platform and default settings.
3. Deploy the WordPress code to the environment.

## Step 4: Configure Security Groups and Environment Properties

1. Add the security group of your Amazon RDS DB instance to your Elastic Beanstalk environment.
2. Configure environment properties for database connection (these match the ones in the sample application):
   - RDS_HOSTNAME
   - RDS_PORT
   - RDS_DB_NAME
   - RDS_USERNAME
   - RDS_PASSWORD

## Step 5: Deploy Your Application

1. Confirm the structure of the wordpress-beanstalk folder.
2. Modify the wp-config.php file to use the environment variables for database connection.
3. Create a source bundle:
   ```sh
   $ zip ../wordpress-beanstalk.zip -r * .[^.]*
   ```
4. Upload the source bundle and deploy it via the Elastic Beanstalk console.

## Step 6: Install WordPress

1. Open the Elastic Beanstalk console and access your environment URL.
2. Go through the WordPress installation wizard, as the wp-config.php file is already configured.

## Step 7: Update Keys and Salts

1. Use the Elastic Beanstalk console to set values for keys and salts as needed.

## Step 8: Remove Access Restrictions

1. Delete the `.ebextensions/loadbalancer-sg.config` file to open the site to the world.
2. Create a new source bundle and deploy it to the environment.

## Step 9: Configure Auto Scaling Group

1. Configure your Elastic Beanstalk environment's Auto Scaling group with a higher minimum instance count (at least 2).

## Step 10: Upgrade WordPress

1. To upgrade WordPress, back up your site and deploy it to a new environment.

## Step 11: Additional Configurations

1. Configure a custom domain name for your production environment.
2. Enable HTTPS for secure connections.

## Step 12: Clean Up

1. Terminate your Elastic Beanstalk environment.
2. Terminate your Amazon RDS DB instance.

## Conclusion

This guide covered deploying a high-availability WordPress website using an external Amazon RDS database. By using this approach, you can achieve decoupling between your database and environment, ensuring flexibility and scalability.
