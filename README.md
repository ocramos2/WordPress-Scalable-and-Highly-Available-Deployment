# Scalable-and-Highly-Available-WordPress-Deployment

This project demonstrates how to deploy a high-availability WordPress website with an external Amazon RDS database to Elastic Beanstalk.

## Overview

In this project, we will launch a DB instance in Amazon RDS, download WordPress, launch an Elastic Beanstalk environment, configure security groups and environment properties, configure and deploy our application, install WordPress, update keys and salts, remove access restrictions, configure our Auto Scaling group, upgrade WordPress, and clean up.

## Prerequisites

- An AWS account
- Basic knowledge of Elastic Beanstalk operations and the Elastic Beanstalk console

## Steps

1. **Launch a DB instance in Amazon RDS**: When you launch an instance with Amazon RDS, it's completely independent of Elastic Beanstalk and your Elastic Beanstalk environments, and will not be terminated or monitored by Elastic Beanstalk. This allows you to connect to the same database from multiple environments, swap out one database for another, or perform a blue/green deployment without affecting your database.
    1. Sign in to the AWS Management Console.
    2. In the console search bar at the top of the page, search for **RDS**.
    3. On the RDS dashboard, choose **Create database**.
    4. Choose **Standard Create**.
    5. For Engine options, choose **MySQL**.
    6. For Templates, choose **Free tier**.
    7. Enter a name for your DB instance (e.g., `wordpress-db`).
    8. Enter a master username (e.g., `admin`).
    9. Enter a master password and confirm it.
    10. Choose **Create database**.

2. **Download WordPress**: You will need to download the WordPress software to your local machine. This tutorial was developed with WordPress version 4.9.5 and PHP 7.0. For current information about the compatibility of PHP releases with WordPress versions, see PHP Compatibility and WordPress Versions on the WordPress website.

3. **Launch an Elastic Beanstalk environment**: You will need to launch an Elastic Beanstalk environment to host your WordPress website. This tutorial assumes you have knowledge of the basic Elastic Beanstalk operations and the Elastic Beanstalk console. If you haven't already, follow the instructions in Getting started using Elastic Beanstalk to launch your first Elastic Beanstalk environment.

4. **Configure security groups and environment properties**: You will need to configure the security groups and environment properties for your Elastic Beanstalk environment and Amazon RDS DB instance to allow communication between the two.
    1. Sign in to the AWS Management Console.
    2. In the console search bar at the top of the page, search for **EC2**.
    3. On the EC2 dashboard, choose **Security Groups** from the navigation menu on the left side of the page.
    4. Find the security group associated with your Elastic Beanstalk environment (e.g., `awseb-e-...`) and choose its name.
    5. Choose **Inbound rules**.
    6. Choose **Edit inbound rules**.
    7. Choose **Add rule**.
    8. For Type, choose **MySQL/Aurora**.
    9. For Source, choose **Custom** and enter the CIDR block associated with your VPC (e.g., `172.31.0.0/16`).
    10. Choose **Save rules**.

5. **Configure and deploy your application**: You will need to configure your WordPress application and deploy it to your Elastic Beanstalk environment.

6. **Install WordPress**: After deploying your application, you will need to install WordPress by accessing the website and following the installation prompts.

7. **Update keys and salts**: You will need to update the keys and salts in your `wp-config.php` file for added security.

8. **Remove access restrictions**: You will need to remove any access restrictions that you may have set during the installation process.

9. **Configure your Auto Scaling group**: You can configure your Auto Scaling group to automatically scale your environment based on demand.

10. **Upgrade WordPress**: You can upgrade your WordPress installation by following the instructions provided by WordPress.

11. **Clean up**: When you are finished with your project, you can clean up by terminating your Elastic Beanstalk environment and deleting your Amazon RDS DB instance by following these steps:
    1. Sign in to the AWS Management Console.
    2. In the console search bar at the top of the page, search for **Elastic Beanstalk**.
    3. On the Elastic Beanstalk dashboard, choose **Environments** from the navigation menu on the left side of the page.
    4. Find your environment and choose its name.
    5. Choose **Actions** and then **Terminate environment**.
    6. In the console search bar at the top of the page, search for **RDS**.
    7. On the RDS dashboard, choose **Databases** from the navigation menu on the left side of the page.
    8. Find your DB instance and choose its name.
    9. Choose **Actions** and then **Delete**.

## Conclusion

In this project, we demonstrated how to deploy a high-availability WordPress website with an external Amazon RDS database to Elastic Beanstalk. By following these steps, you can create a scalable and reliable WordPress website that can handle high levels of traffic.
