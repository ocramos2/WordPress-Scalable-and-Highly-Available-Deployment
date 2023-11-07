# Scalable and Highly-Available WordPress Deployment

## Overview
This guide provides steps to deploy a highly available WordPress website on AWS Elastic Beanstalk with Amazon RDS for robust performance. By following these steps, you can create a scalable and reliable WordPress website that can handle high levels of traffic.

## WordPress Setup
- Download and extract WordPress from the official WordPress website.
- Compress all files inside the extracted folder.
- Move the new `wordpress.zip` to the Desktop for upload.

## IAM Role Creation
1. Open IAM on a separate tab.
2. On the left menu, choose "Roles".
3. Click on "Create role" and name it `aws-elasticbeanstalk-service-role`.
4. Under Trusted entity type, choose AWS service.
5. Under Use case, choose Elastic Beanstalk.
6. For Choose a use case for the specified service, select Elastic Beanstalk.
7. Click on Next.
8. Under permission policies, use `AWSElasticBeanstalkServiceRolePolicy`.
9. Click on Next.
10. Under Name, review, and create, click on Create role.

Repeat the above steps to create another role named `aws-elasticbeanstalk-ec2-role` with the following changes:
- In step 5, choose EC2 for the Use case.
- In step 8, use `AmazonS3FullAccess` and `CloudWatchAgentServerPolicy` for the permission policies.

## Elastic Beanstalk Setup
1. Open Elastic Beanstalk.
2. On the left menu, choose "Applications".
3. Click on "Create application".
4. Choose a name for "Application name".
5. Click on "Create".
6. On the left menu, choose "Environments".
7. Click on "Create environment".
8. Under Environment tier, choose Web server environment.
9. Under Application name, write a name of your choice (ie wordpress).
10. Under Platform, choose PHP.
11. Leave default settings.
12. Under Application code, you can choose Sample application or Upload your code.
13. If you upload your code, choose Local file.
14. Then upload the `wordpress.zip` file you created.
15. Under Version label, type `v1`.
16. Under Presets, choose Single instance (free tier eligible).
17. Click Next.

## Service Access and VPC Settings
1. Under Service access, choose Use an existing service role.
2. Under Existing service roles, choose `aws-elasticbeanstalk-service-role`.
3. Under EC2 instance profile, choose `aws-elasticbeanstalk-ec2-role`.
4. Click Next.
5. Under VPC, choose the default VPC.
6. Under Instance subnets, choose two availability zones (i.e. us-east-1a and us-east-1b).
7. Under Choose database subnets, choose two availability zones (i.e. us-east-1a and us-east-1b).
8. Toggle the enable database button.
9. Under Database settings, choose mysql as Engine, db.t2.micro as instance class, 5 as Storage, a username, a password, Low (one AZ) as Availability, Delete as Database deletion policy.
10. Click Next.
11. Under EC2 security groups, choose default.
12. Under Fleet composition, On-demand instance.
13. Under instance types, choose t3.micro.
14. Click Next.
15. Under Health reporting, choose Basic.
16. Click Next.
17. Under Review, click Submit.

Wait until the Elastic Beanstalk environment finishes launching. Under Environment overview, Health should be Green. Under Domain, click on the link. You should see a WordPress page. Select a language and click Continue. Click on Let's go!

## Database Setup
1. Open RDS on a separate tab.
2. On the left menu, choose "Databases".
3. Choose the database you just created.
4. Under Configuration, find DB name.
5. Under Connectivity & security, find the Endpoint.

Go back to the WordPress page. Enter the following information: Database=wordpress, Username=ebdb, Password=any 8-characters, Database Host=Endpoint. Click Submit.

## Clean Up
Terminate S3, EC2, RDS, and Elastic Beanstalk instances.

In this project, we demonstrated how to deploy a high-availability WordPress website with an external Amazon RDS database to Elastic Beanstalk. By following these steps, you can create a scalable and reliable WordPress website that can handle high levels of traffic.

## Acknowledgment
This tutorial is adapted from the [AWS Elastic Beanstalk tutorial for deploying a high-availability WordPress website](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/php-hawordpress-tutorial.html) provided by Amazon Web Services. We extend our gratitude to AWS for providing this valuable resource, which served as the foundation for the "Scalable and Highly-Available WordPress Deployment" tutorial.
