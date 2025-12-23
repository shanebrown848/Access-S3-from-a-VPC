# Access S3 from a VPC

**Project Link:** https://learn.nextwork.org/projects/aws-networks-s3  
**Author:** Shane Brown  

---

## Overview

This project focuses on accessing Amazon S3 from within an Amazon Virtual Private Cloud (VPC). The goal is to understand how resources inside a VPC interact with AWS services outside the VPC and how authentication and permissions enable that access.

This project connects networking fundamentals with identity and access management concepts.

---

## What I built

I created a VPC-based environment and configured secure access from an EC2 instance to Amazon S3. This included:

- Creating a custom VPC and public subnet  
- Launching an EC2 instance inside the VPC  
- Connecting to the instance using EC2 Instance Connect  
- Creating an Amazon S3 bucket and uploading objects  
- Configuring AWS CLI credentials on the EC2 instance  
- Accessing and managing S3 objects from within the VPC  

This setup demonstrates how compute resources inside a VPC interact with managed AWS services.

---

## Key concepts learned

- How resources inside a VPC access AWS services like S3  
- Why EC2 instances do not automatically have AWS permissions  
- How access keys authenticate AWS CLI requests  
- How the AWS CLI is used to interact with S3  
- Security considerations when using access keys  
- Why IAM roles are the preferred production approach  

---

## Accessing S3 from an EC2 instance

I used the AWS CLI from an EC2 instance to interact with Amazon S3. After configuring credentials with `aws configure`, I was able to:

- List all S3 buckets in my account  
- View objects inside a specific S3 bucket  
- Upload new files from the EC2 instance to S3  

This confirmed that resources inside a VPC can securely interact with AWS services when properly authenticated.

---

## Credentials and security

To enable S3 access, I configured access keys on the EC2 instance. Access keys consist of an access key ID and a secret access key, which allow the AWS CLI to authenticate requests.

While access keys were used for this project, a best practice in real-world environments is to use IAM roles attached to EC2 instances. IAM roles provide temporary credentials, rotate automatically, and reduce the risk of credential exposure.

---

## Why this project matters

Accessing AWS services from within a VPC is a common requirement in cloud environments. Understanding how authentication, permissions, and networking work together is critical for building secure and functional cloud architectures.

This project demonstrates how networking, compute, and identity services intersect in AWS.

---

## Documentation

📄 **Full project documentation:**  
[documentation.md](./documentation.md)

This file includes setup steps, CLI commands, test results, and reflections from completing the project.

---

## Credits

Built as part of the **NextWork** AWS networking learning series.
