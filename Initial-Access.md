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
