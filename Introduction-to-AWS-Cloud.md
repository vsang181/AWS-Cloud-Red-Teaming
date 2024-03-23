# Introduction to AWS Cloud

AWS stands for “Amazon Web Services”  is a complex and evolving cloud computing platform by Amazon that offers a variety of services which include-

- Infrastructure as a service (Iaas)
- Platform as a service (Paas)
- Software as a service (SaaS)

## Regions & Availability Zones (AZs)

Regions are the physical locations of the cluster of data centers around the world. Each AWS Region consists of a minimum of three, isolated, and physically separate AZs within a geographic area. At the moment of writing there are 33 regions available.

An Availability Zone (AZ) with one or more discrete data centers with redundant power, networking and connectivity in an AWS region. At the time of writing there are 105 AZs available.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/3aa9a1ba-f66f-4139-a354-176cae67a2fc)

## AWS Services Access

There are three ways to access the services provided by AWS-

- **AWS management Console**: It provides a web based user interface that allow us to create and manage AWS resources.
- **AWS CLI (Command Line Interface)**: It is a command line tool to create and manage AWS resources. Whcih can be access just by installing one tool which is [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).
- **AWS SDK (Software Development Kits)**: It provides an abstract of APIs from AWS services for the developers to implement in their application development process or use it based on the requirements accordingly.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/6f78a9f4-46a6-4be0-a0f2-61916755aaca)

## AWS Cloud Architecture

There two basic things to know here first-

1. Cloud Space
2. User Space

In the **User Space** it contains the three ways we learned above to access the functionalists in Cloud Space.

In the **Cloud Space** it has the GUI which interact with the web client and AWS services which interact with the AWS CLI & SDK/API.

Which then interact with the Data plane where the actual work happens i.e. Computation and storage functionality.

## AWS Cloud Service Model:

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/42d5605a-11ec-4dfa-96ac-dcf47d6de34f)

## AWS Cloud Services Uses

These are some of the Basic service use cases provided by AWS and the actual use cases may not be limited to the ones only mentioned in the list bellow.

- Networking
  - Virtual private cloud (VPC

- Access Management
  - Identity and Access Management (IAM)
  
- Compute
  - Elastic Compute Cloud (EC2)
  - Container
  - Lambda  
  
- Storage
  - Simple Storage Service (S3)
  - Relational Database Service (RDS)
  - Elastic Book Store (EBS)
  - DynamicDB

- Security Services
  - Inspector
  - Guard Duty
  - Cloud Trail
  - WAP
 
## Let's Connect

I welcome your insights, feedback, and opportunities for collaboration. Together, we can make the digital world safer, one challenge at a time.

- **LinkedIn**: (https://www.linkedin.com/in/aashwadhaama/)

I look forward to connecting with fellow cybersecurity enthusiasts and professionals to share knowledge and work together towards a more secure digital environment.
