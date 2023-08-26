# Scalable and Highly-Available WordPress Deployment

Deploy a resilient WordPress website with Amazon RDS and Elastic Beanstalk using streamlined, comprehensive instructions.

## Overview

This guide offers efficient steps to deploy a highly available WordPress website on Elastic Beanstalk, integrating an Amazon RDS database for robust performance.

## Prerequisites

- AWS account
- Basic familiarity with Elastic Beanstalk operations and AWS console navigation

## Steps

1. **Launch an Amazon RDS DB Instance**:
   - Log in to the [AWS Management Console](https://aws.amazon.com/console/).
   - Search for "RDS" and access the Amazon RDS dashboard.
   - Click "Create database."
   - Choose "Standard Create."
   - Select "MySQL" for "Engine options."
   - Opt for the "Free tier" template.
   - Enter a unique name (e.g., `wordpress-db`) as the "DB instance identifier."
   - Set a master username (e.g., `admin`).
   - Create a strong master password and confirm it.
   - In "Additional configuration," set "Database port" to `3306`.
   - Click "Create database."
   - Wait for the DB instance to transition to "Available."

2. **Download WordPress**:
   - Download the latest WordPress version from the [official website](https://wordpress.org/).
   - Extract the ZIP file to a local folder.

3. **Launch an Elastic Beanstalk Environment**:
   - Log in to the AWS Management Console.
   - Search for "Elastic Beanstalk" and access the Elastic Beanstalk dashboard.
   - Click "Create a new environment."
   - Choose "Web server environment."
   - Select a platform supporting PHP (e.g., "PHP").
   - Click "Configure more options."
   - Under "Software," click "Edit."
   - Set "Document root" to `/wordpress`.
   - Click "Save" and continue with configuration.

4. **Configure Security Groups and Environment Properties**:
   - In the AWS Management Console, search for "EC2" and access the EC2 dashboard.
   - Go to "Security Groups."
   - Locate the security group associated with your Elastic Beanstalk environment (e.g., `awseb-e-...`).
   - Edit inbound rules and add a rule:
     - For "Type," select "MySQL/Aurora."
     - For "Source," choose "Custom" and input your VPC's CIDR block (e.g., `172.31.0.0/16`).
   - Save rules.

5. **Configure and Deploy Your Application**:
   - Open `wp-config.php` from the extracted WordPress folder.
   - Replace `localhost` in `DB_HOST` with your RDS endpoint.
   - Replace placeholders in `DB_NAME`, `DB_USER`, and `DB_PASSWORD` with RDS details.
   - Save the file.
   - Create a ZIP file of the WordPress files.
   - In Elastic Beanstalk, navigate to your environment and upload the ZIP file for deployment.

6. **Install WordPress**:
   - Access the deployed website URL.
   - Follow on-screen instructions for WordPress installation.

7. **Enhance Security with Keys and Salts**:
   - Generate new keys and salts using the [WordPress Secret Key Generator](https://api.wordpress.org/secret-key/1.1/salt/).
   - Replace existing keys and salts in `wp-config.php`.

8. **Seamless Access**:
   - Remove any installation-related access restrictions.

9. **Optimize Scaling**:
    * Configure Auto Scaling settings based on traffic variations.

10. **Stay Updated**:
    * Regularly update WordPress for performance and security enhancements.

11. **Resource Management and Clean Up**:
    - When you're finished with your project, ensure proper resource management:
      - Terminate your Elastic Beanstalk environment:
        1. In the AWS Management Console, search for "Elastic Beanstalk."
        2. On the Elastic Beanstalk dashboard, choose "Environments" from the navigation menu.
        3. Find your environment, choose its name, then click "Actions" and "Terminate environment."
      - Delete your Amazon RDS DB instance:
        1. In the AWS Management Console, search for "RDS."
        2. On the RDS dashboard, choose "Databases" from the navigation menu.
        3. Find your DB instance, choose its name, then click "Actions" and "Delete."

## Conclusion

In this project, we demonstrated how to deploy a high-availability WordPress website with an external Amazon RDS database to Elastic Beanstalk. By following these steps, you can create a scalable and reliable WordPress website that can handle high levels of traffic.

## Acknowledgment

This tutorial is adapted from the [AWS Elastic Beanstalk tutorial for deploying a high-availability WordPress website](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/php-hawordpress-tutorial.html) provided by Amazon Web Services. We extend our gratitude to AWS for providing this valuable resource, which served as the foundation for the "Scalable and Highly-Available WordPress Deployment" tutorial.
