# Identity and Access Management (IAM)

## Introduction

Identity and Access management refers to the practice of making sure only the authorised individuals/users have the access to the right organisational resources or data.

Here, AWS IAM allows to create and manage users & groups and manage permissions to allow or deny access to the AWS resources.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/f96c4fdc-ce3d-4e25-8c69-0da15ca3febf)

**AWS IAM allows -**

- Manage users, groups and their access.
- Manage roles and their permissions.
- Manage federated users and their permissions.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/390e256d-a226-437d-b407-6b16d26af75c)

## Service Access Types

1. Programmatic Access

- Access Key ID
- Secret Access Key

2. AWS Management Console Access

- Username
- Password

> Amazon Resource Names (ARNs): To uniquely identify AWS resources. [Aamaon's User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference-arns.html) 

> Temporary Credentials include; Access Key ID, Secret Access Key and Security token (session token).  

**Users**

An entity in AWS to represent a person or an application that interact with the AWS. It consist of a name and credentials.

**Groups**

 An entity in AWS to represent a collection of users. It lets us to specify permissions for a set of users, which make it easier when dealing with changing or applying new rules or permissions to a large number of users.
 
A group contain multiple users and a user can belong to multiple groups. Groups can not be nested i.e. it can only contain users not other groups.

**Roles**

An entity that define a set of permissions allowing to make AWS service requests. IAM Roles are considerably secure ways to grant permissions to entities within AWS as it issues keys only valid for set period of time. An example of Roles is when a application running on EC2 instance need to pull a file from S3 Bucket only roles can be used to do such, allowing one service of AWS to access another.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/d604e546-c7cf-4549-83bc-7be208366d69)

**Policies**

An entity in AWS which does the actual permission defining. For example if a policy allows GetUser action, then the users having those policies assigned to can perform this action and obtain user information. It can be attached to any of the IAM identities discussed above.

Policy Data-
- Effect: To Allow or Deny Access to a list of actions.
- Action:  A list of actions like GET, Put, Delete, etc.
- Resource: A list of resources to which the actions apply.

Policy types-

- AWS Managed Policies: A standalone policy created by AWS. It has its own ARN.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/713cb176-7d8b-4097-8111-05158b93fd9e)

- Customer Managed Policies: Standalone polices in user's own AWS account that can attach to principal identities. user can create these for specified use cases while having the ability to change or update them as often as required. Same as AWS managed policies but created by the user.

- Inline Policies: Created by a single IAM identity to maintain a strict one to one relationship between the IAM identity and the policy. They get removed when we delete the identity

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/ad6771fc-c40e-48e4-800a-5a264328f255)

**Security Token Services (STS)**

An entity in AWS used to create temporary access to an AWS recourse and grant it to a user.

Types of temporary crentials-
- STS: https://sts.amazonaws.com (Users or other AWS Account Users/Services)
- AWS Metadata: - http://<IP> (IAM Roles - Same AWS Account)

## Exploitation

### Enumeration

To perform any users we need to be authenticated first.

```
aws configure
```

We need a minimum read access on the AWS resources to enumerate.

If we have a AWS key but not know which user it belongs to.

```
aws sts get-caller-identity
```

![Screenshot 2024-03-16 015556](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/2047070d-4a66-424e-ae6f-202521b42e47)

#### Users

- List of IAM Users

```
aws iam list-users
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/50554820-eb73-497d-87c9-39c0a37a9b8e)

- List of IAM groups that the specified IAM user belongs to 

```
aws iam list-groups-for-user --user-name <user name>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/a1e26b25-7de7-496b-930e-6c84e537ddb4)

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/6aadfe7a-3f08-4231-a157-70138fa44b9d)

- List of managed policies that are attached to specified IAM user

```
aws iam list-attached-user-policies --user-name <username>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/b22fe468-89f0-418a-9614-5a1725f075a6)

- Lists the names of the inline policies embedded in the specified IAM user :

```
aws iam list-user-policies --user-name <username>
```

#### Groups

- List of IAM Groups:

```
aws iam list-groups
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/29793801-642c-4dc3-ab71-484d972ab856)

- Lists all managed policies that are attached to the specified IAM Group :

```
aws iam list-attached-group-policies --group-name <group name>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/b85ce3fd-fd8a-4c28-a311-5112e5179a56)

- List the names of the inline policies embedded in the specified IAM Group: 

```
aws iam list-group-policies --group-name group-name
```

#### Roles

- List of IAM Roles :

```
aws iam list-roles
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/112b98ae-d99a-4332-afee-c5f2d2830424)

- Lists all managed policies that are attached to the specified IAM role :

```
aws iam list-attached-role-policies --role-name <role name>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/964e17ab-4564-4f4c-afc7-431470def6ea)

- List the names of the inline policies embedded in the specified IAM role : 

```
aws iam list-role-policies --role-name <role name>
```

#### Policies

- List of IAM Policies :

> Note: In AWS a policy can only have 5 versions to it.

```
aws iam list-policies
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/3f93c0ec-95ea-4d59-851a-72ac4df0db11)

- Retrieves information about the specified managed policy : 

```
aws iam get-policy --policy-arn <policy arn>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/95c69ec5-32f9-4efd-aa3f-b5e44e87ab66)

- Lists information about the versions of the specified manages policy :

```
aws iam list-policy-versions --policy-arn <policy arn>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/745a4ddf-d1d1-453b-9249-212566fafe90)

- Retrieved information about the specified version of the specified managed policy : 

```
aws iam get-policy-version --policy-arn <policy arn> --version-id <version id>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/d4a303e6-34fc-42c8-b88a-bad56d533d28)

- Retrieves the specified inline policy document that is embedded on the specified IAM user / group / role :

```
aws iam get-user-policy --user-name <user name> --policy-name <policy name>
aws iam get-group-policy --group-name <group name> --policy-name <policy name>
aws iam get-role-policy --role-name <role name> --policy-name <policy name>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/b046c131-0c5d-4fc1-a389-919867986378)

### Initial Access

We have 3 ways to access an AWS cloud environment as defined before.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/ed61ca81-8b8c-4f52-8e90-f1fe21bfe79b)

- Console sign in URL for root User :

```
https://signin.aws.amazon.com/console
```

- Console sign in URL for IAM User :

```
https://account-ID-or-alias.signin.aws.amazon.com/console
```

- Configure AWS CLI :

```
aws configure --profile <profile name>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/a48e3649-969d-495e-b4c5-6d4a731b3870)

Here when we try to configure via CLI for a user named `demo` we are asked for a `AWS Access Key ID`.

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/8d0c34a5-2292-4331-b824-9d9219fdbfdd)

Then we are asked for a `AWS Secret Key`.

> Note: All access keys for the users configured are stored in the hidden folder named `aws` of the user on windows used while configuring in the file  named `credentials`.

### Persistence

To create a back door if the `User 1` is compromised and have enough privileges, we can create a new access key for a user which is less likely to be suspicious or managed.   

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/5a7a2477-ad2b-4b1c-8e5c-2183317b8966)

> Note: A user in AWS cloud environment can only have 2 access keys at a time.

- Creates a new AWS secret access key for IAM User :

```
aws iam create-access-key --user-name <username>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/3d634516-5aa9-478f-9c13-5e2def0d8752)

- Configure AWS CLI for New User :

```
aws configure --profile <profile name>
```

![image](https://github.com/vsang181/AWS-Cloud-Red-Teaming/assets/28651683/8896b55a-482f-4393-b91c-0de583e7fefa)
















.
.
.
.
.
.
_In progress..._
