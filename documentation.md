<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Access S3 from a VPC

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-s3)

**Author:** Shane Brown  
**Email:** shanebrown848@gmail.com

---

## Access S3 from a VPC

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-s3_3e1e79a2)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that lets you create your own logically isolated network inside the AWS Cloud, where you control things like IP address ranges, subnets, routing, and security. It is useful because it gives you a secure and customizable environment to launch and manage AWS resources, such as EC2 instances, while controlling how they communicate with each other and with services outside the VPC, like the internet or Amazon S3.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create a private network environment where I launched an EC2 instance in a public subnet and controlled its networking setup. I then used this VPC-based EC2 instance to securely connect to and interact with Amazon S3 using the AWS CLI, showing how resources inside a VPC can access AWS services outside the VPC.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was that an EC2 instance cannot access AWS services like S3 by default, even though it is already running inside my AWS account. I was surprised that I had to explicitly provide credentials using access keys before the instance could interact with S3 through the AWS CLI.

### This project took me...

This project took me about 1 hour, I took my time, there was alot of detail I didn't want to miss.

---

## In the first part of my project...

### Step 1 - Architecture set up

In this step, I am setting up the foundation for the project by creating a new VPC and launching an EC2 instance inside it. I’m doing this so I have a secure network environment and a running server that I can later use to test how resources inside a VPC access AWS services like Amazon S3.

### Step 2 - Connect to my EC2 instance

In this step, I connected directly to my EC2 instance using EC2 Instance Connect through the AWS Management Console. This gave me secure, browser-based SSH access to the instance’s terminal without needing to manage my own key pair. By successfully connecting to the EC2 instance, I confirmed that the instance is reachable, has a public IP address, and is correctly set up to interact with AWS services in the next steps of the project.

### Step 3 - Set up access keys

In this step, I set up credentials so my EC2 instance can securely access AWS services. Since the EC2 instance acts like its own user, it needs access keys to authenticate with AWS when using tools like the AWS CLI. By creating and configuring access keys, I gave the instance permission to interact with my AWS environment, which allows it to perform actions such as listing and managing Amazon S3 resources directly from the terminal.

---

## Architecture set up

In this step, I created a new VPC using the VPC wizard and then launched an EC2 instance inside it. I configured the VPC with a single public subnet, no private subnets, no NAT gateway, and default networking settings. I then launched an Amazon Linux EC2 instance in the public subnet with a public IPv4 address and a basic security group that allows SSH access, so I can connect to the instance using EC2 Instance Connect and use it later to access Amazon S3.

In this step, I created an Amazon S3 bucket in the same AWS Region as my VPC so it could be accessed later from my EC2 instance. I gave the bucket a unique name and kept all the default settings. After the bucket was created, I uploaded two files from my local computer into the bucket. This gives me real objects stored in S3 that I can use to test access and interaction from inside my VPC using the AWS CLI.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-s3_4334d777)

---

## Running CLI commands

AWS CLI is a command-line tool that lets you interact with AWS services by typing commands in a terminal instead of clicking around in the AWS Management Console. It allows you to do things like list S3 buckets, upload files, or manage resources directly from the command line. I have access to the AWS CLI because it comes preinstalled on my EC2 instance, which allows the instance to run AWS commands once I provide the required credentials.

The first command I ran was aws s3 ls. This command is used to list all the Amazon S3 buckets in my AWS account that the current credentials have permission to access.

The second command I ran was aws configure. This command is used to set up AWS credentials and configuration settings, such as the access key ID, secret access key, default region, and output format, so the EC2 instance can authenticate with AWS services when running AWS CLI commands.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-s3_e7fa8776)

---

## Access keys

### Credentials

To set up my EC2 instance to interact with my AWS environment, I configured the AWS CLI by providing my access key ID, secret access key, default region, and output format. Running the aws configure command stored these credentials on the EC2 instance so it could authenticate with my AWS account and make authorized requests to services like Amazon S3.

Access keys are credentials used by applications, scripts, or servers to securely authenticate with AWS services. They are made up of two parts: an access key ID, which acts like a username, and a secret access key, which acts like a password. Together, they allow tools like the AWS CLI running on an EC2 instance to prove who they are and get permission to interact with AWS resources such as Amazon S3, based on the permissions assigned to the IAM user or role they belong to.

Secret access keys are the private, sensitive part of an AWS access key pair that work together with the access key ID to authenticate and authorize access to AWS services. They function like a password and must be kept secure, because anyone who has both the access key ID and the secret access key can use them to access your AWS account and its resources with the permissions assigned to that user or role.

### Best practice

Although I’m using access keys in this project, a best practice alternative is to use IAM roles attached to EC2 instances. IAM roles let the instance automatically receive temporary credentials without storing access keys on the server. This is more secure because credentials are rotated automatically, never hard-coded, and can’t be accidentally exposed if someone gains access to the instance.

---

## In the second part of my project...

### Step 4 - Set up an S3 bucket

In this step, I created an Amazon S3 bucket so I would have a resource to access from my EC2 instance. The bucket acts as cloud storage that lives outside of my VPC, which makes it a good example of how resources inside a VPC can interact with other AWS services. After creating the bucket, I’ll use my EC2 instance and the AWS CLI to connect to S3 and verify access by listing and interacting with objects in the bucket.

### Step 5 - Connecting to my S3 bucket

In this step, I went back to my EC2 instance using EC2 Instance Connect and used the AWS CLI to interact with my S3 bucket. After configuring my access keys, the EC2 instance was able to authenticate with my AWS account. I then ran S3 commands from the terminal to list my buckets and view the files inside the bucket I created earlier. This confirmed that my EC2 instance could successfully access and interact with Amazon S3 from inside the VPC.

---

## Connecting to my S3 bucket

The first command I ran was aws s3 ls. This command is used to list all the Amazon S3 buckets in my AWS account that the current credentials have permission to access.

After configuring my AWS credentials, I ran the aws s3 ls command again from my EC2 instance. This time, the command successfully returned a list of S3 buckets in my AWS account, including the bucket I created for this project. This confirmed that my EC2 instance was properly authenticated and now had permission to interact with Amazon S3 using the AWS CLI.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-s3_4334d778)

---

## Connecting to my S3 bucket

Another CLI command I ran was aws s3 ls s3://nextwork-vpc-project-<my-name>, which returned a list of the objects stored inside my S3 bucket, including the files I uploaded earlier. This confirmed that my EC2 instance could successfully access and read data from the bucket using the AWS CLI.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-s3_4334d779)

---

## Uploading objects to S3

To upload a new file to my bucket, I first ran the command sudo touch /tmp/test.txt. This command creates an empty text file named test.txt in the /tmp directory on my EC2 instance, which I could then upload to Amazon S3 using the AWS CLI.

The second command I ran was aws s3 cp /tmp/test.txt s3://nextwork-vpc-project-yourname. This command uploads the test.txt file from my EC2 instance to my Amazon S3 bucket by copying it from the local /tmp directory into the specified S3 bucket.

The third command I ran was aws s3 ls s3://nextwork-vpc-project-yourname, which validated that the file upload was successful by listing the objects in the S3 bucket and showing that test.txt now exists in the bucket.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-s3_3e1e79a2)

---

---
