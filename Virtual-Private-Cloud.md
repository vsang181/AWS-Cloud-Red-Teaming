# Virtual Private Cloud (VPC)

## Introduction

Amazon Virtual Private Cloud (Amazon VPC) lets a user to launch AWS resources in a logically isolated network. A user have complete control over virtual networking environment, including selection of IP address range, creating of subnets, and configuration of route tables and network gateways.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/969c4694-26bb-48fe-af71-51154f63f951)

### Subnets

A subnet is a range of IP addresses in your VPC. You can create AWS resources, such as EC2 instances, in specific subnets.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/038d5fac-7b7c-4b1f-8b39-e9cd5664fb6d)

### Routing Tables

A route table contains a set of rules, called `routes`, that determine where network traffic from your subnet or gateway is directed.

|Destination|Target|
|---|---|
|IP Address|Local|
|IP Address|Interntet Gateway (igw)|
|IP Address|Nat Gateway (nat)|
|IP Address|VPC Peering (pcx)|
|IP Address|VPC Endpoint (vpce)|
|IP Address|VPN Gateway (vgw)|
|IP Address|Network Interface (eni)|

### Internet Gateway

An internet gateway is a VPC component that allows communication between your VPC and the internet. It supports IPv4 and IPv6 traffic. It does not cause availability risks or bandwidth constraints on user's network traffic.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/b3c4b35c-2ed7-4e30-8d85-4423fcdab464)

### NAT Gateway

A NAT gateway is a Network Address Translation (NAT) service. Can be used so that instances in a private subnet can connect to services outside the VPC but external services cannot initiate a connection with those instances.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/7dfef54e-6bcc-4325-b7f0-e51d3f429eb9)

### VPC Peering

A VPC peering connection is a networking connection between two VPCs that enables you to route traffic between them using private IPv4 addresses or IPv6 addresses.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/86ef26f6-520b-4f9d-85c7-3f835975f057)

### VPC Endpoints

A VPC endpoint enables customers to privately connect to supported AWS services and VPC endpoint services powered by AWS PrivateLink.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/ad253e62-1dab-454b-8e50-068cf676b76e)

### Network ACLs

A network access control list (ACL) allows or denies specific inbound or outbound traffic at the subnet level. Can be used with the default network ACL for the VPC, or a custom network ACL can be created for the VPC with rules that are similar to the rules for security groups in order to add an additional layer of security to your VPC.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/84db2894-7c56-4f66-820e-6219d8c9c455)

## Exploitation

### Enumeration

- Describe about VPCs :
 
> There is at least a read only access required for bellow command and we can also define the region by adding the `--region us-west-1`. 

```
aws ec2 describe-vpcs
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/14b15bfe-9471-44e5-8c57-a9294b937f2e)

- Describe a specified VPC:

```
aws ec2 describe-vpcs --filters "name=vpc-id, Values=<vpc id>"
```

- Describe about all Subnets in default region:

```
aws ec2 describe-subnets
```

- Describe about Subnets for specified VPC:

```
aws ec2 describe-subnets --filters="name=vpc-id, Values=<vpc id>"
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/95b8a5c9-4f98-4764-a62f-57047f91c2dd)

- Describe about Route Table :

> The same filter as above can be used to filter based on specified "vpc-id" or "subnet-id". 

```
aws ec2 describe-route-tables
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/dc52dee3-a574-41f3-9bf8-f7f5647b13de)

- Describe about all Network ACLs :

```
aws ec2 describe-network-acls
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/554bd7be-0ca3-4205-8820-fc77115c9725)

### Lateral Movement / Pivoting

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/b06d3a55-182e-4209-b509-51c816d44a3a)

> There is at least a read only access required for bellow command.

- Describes all VPC Peering Connections :

```
aws ec2 describe-vpc-peering-connections
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/bf8f34c8-675a-4557-b09e-22de9c9ebcad)

- Describe about Subnet of the specified VPC :

```
aws ec2 describe-subnets --filters “Name=vpc-id, Values=<vpc id>”
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/8167f7f3-09ce-404b-a3ce-25c56f5ba36e)

- Describe about Route Table of the specified Subnet :

```
aws ec2 describe-route-tables --filters “Name=vpc-id, Values=<vpc id>”
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/1f4548bb-2638-42aa-98d8-b090f65de397)

- Describe about Network ACL of the specified VPC :

```
aws ec2 describe-network-acls --filters “Name=vpc-id, Values=<vpc id>”
```

- Describe about EC2 Instances In the specified VPC :

```
aws ec2 describe-instances --filters “Name=vpc-id, Values=<vpc id>”
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/1fef997b-365e-4005-acdc-34b98f36cfe0)

- Describe about EC2 Instances In the specified Subnet:

```
aws ec2 describe-instances --filters “Name=subnet-id, Values=<subnet id>"
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/9f08405c-83df-40f0-b64a-70dc856856c8)

.
.
.
.
.
.
_In progress..._

## Let's Connect

I welcome your insights, feedback, and opportunities for collaboration. Together, we can make the digital world safer, one challenge at a time.

- **LinkedIn**: (https://www.linkedin.com/in/aashwadhaama/)

I look forward to connecting with fellow cybersecurity enthusiasts and professionals to share knowledge and work together towards a more secure digital environment.
