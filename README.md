# Scalable and Highly-Available WordPress Deployment

## Overview
This guide provides steps to deploy a highly available WordPress website on AWS Elastic Beanstalk with Amazon RDS for robust performance. By following these steps, you can create a scalable and reliable WordPress website that can handle high levels of traffic.

<img width="1440" alt="Wordpress-project" src="https://github.com/ocramos2/WordPress-Scalable-and-Highly-Available-Deployment/assets/90172092/9538a2e1-9f23-4319-ab3b-b3fba8e623bb">

## WordPress Setup
1. Download and extract WordPress from the official WordPress website.
2. Compress all files inside the extracted folder.
3. Move the new `wordpress.zip` to the Desktop for upload.

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
1. In step 5, choose EC2 for the Use case.
2. In step 8, use `AmazonS3FullAccess` and `CloudWatchAgentServerPolicy` for the permission policies.

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
9. Under Database settings, choose mysql as Engine, instance class=db.t2.micro (or t3.micro, which is newer), Storage=5, a username, a password, Availability=Low (one AZ) (multi-AZ means you will incur a fee for high-availability), Database deletion policy=Delete.
10. Click Next.
11. Under EC2 security groups, choose default.
12. Under Fleet composition, On-demand instance.
13. Under instance types, choose t3.micro.
14. Click Next.
15. Under Health reporting, choose Basic.
16. Click Next.
17. Under Review, click Submit.
18. Wait until the Elastic Beanstalk environment finishes launching.
19. Under Environment overview, Health should be Green.
20. Under Domain, click on the link.
21. When you see the WordPress page, select a language and click Continue.
22. Click on Let's go!

## Database Setup
1. Open RDS on a separate tab.
2. On the left menu, choose "Databases".
3. Choose the database you just created.
4. Under Configuration, find DB name.
5. Under Connectivity & security, find the Endpoint address.
6. Go back to the WordPress page.
7. Enter the following information: Database=wordpress, Username=ebdb, Password=any 8-characters, Database Host=Endpoint address.
8. Click Submit.

## Clean Up
Empty and terminate Elastic Beanstalk, RDS, S3 (might need to delete bucket policy), and EC2 instances.

## Conclusion
In this project, we demonstrated how to deploy a high-availability WordPress website with an external Amazon RDS database to Elastic Beanstalk. By following these steps, we have created a scalable and reliable WordPress website that can handle high levels of traffic. Feel free to message me with code improvement suggestions.

## Acknowledgment
This tutorial is adapted from the [AWS Elastic Beanstalk tutorial for deploying a high-availability WordPress website](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/php-hawordpress-tutorial.html) provided by Amazon Web Services. We extend our gratitude to AWS for providing this valuable resource, which served as the foundation for the "Scalable and Highly-Available WordPress Deployment" tutorial.
