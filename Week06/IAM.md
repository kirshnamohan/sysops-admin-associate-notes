# IAM - SECURITY

## Basics
- AWS Identity and Access Management
- Control access to AWS services and resources for users and groups
- No additional charge
- Root user: main user, full access

## Implement and Manage Security Policies
- Users and groups have no access by default
- A policy is an entity that, when attached to an identity or resource, defines their permissions. Ex:
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": "dynamodb:*",
    "Resource": "arn:aws:dynamodb:us-east-2:ACCOUNT-ID-WITHOUT-HYPHENS:table/${aws:username}"
  }
}
- You can use roles to delegate access to users, applications, or services that don't normally have access to your AWS resources. 
- Instead of being uniquely associated with one person, a role is intended to be assumable by anyone who needs it
- Ex. A role that allows ec2 to access s3
- You can configure ec2 to asume a role only on creation

## Ensure Data Integrity and Access Controls when Using the AWS Platform
- MFA (Multi Factor Authentication) - should be on for users who have access to the console and admins
- MFA can be used to API access(buckets, etc.)
- MFA with STS(Secure Token Service): used to get temporary credentials that can be used to make requests against AWS services.
- Not supported by all services. S3, SQS, SNS do support it.
- MFA can be used to prevent accidental deletion on S3 objects

- SAML - Secure Assertive Markup Language: authenticate against Identity providers(AD/Facebook). Authenticate -> assume role -> access to resources.(Federated Users)

## Demonstrate understanding of the shared responsibility model
- AWS: Global Infrastructure(Physical), foundation services, firmware and host updates
- AWS: Security of the cloud. Customer: in the cloud
- User: OS, network, firewall config, SG, customer data.
- RDS, ECS, Lambda: Amazon patchs the OS, etc.

## Demonstrate ability to prepare for security assessment use of AWS





## RESOURCES
- https://aws.amazon.com/iam/


### QUIZ

1)In the shared responsibility model, what is AWS's responsibility?

A: Restricting access to the data centres, proper destruction of decommissioned disks, managing security groups for users.
B: Managing security groups for users, Managing OS Level Patches.
C: Creating IAM roles and managing this for AWS users.
D: Restricting access to the data centres, proper destruction of decommissioned disks, patching of firmware for the hardware on which your AWS resources reside.

2)What is the name of the service to allow users to use their social media account to gain temporary access to the AWS platform?

A: Active Directory Authentication Services
B: Web Confederation Services
C: Web Identity Federation
D: Facebook Sign In Service

3)What is the name of the API call to request temporary security credentials from the AWS platform when federating with Active Directory?

A: GetSAMLRole
B: ShowMeTheSAML
C: AssumeRoleWithSAML
D: CovertRoleToSAML

4)When using active directory to authenticate to AWS what are the correct steps performed?

A: 1) The user navigates to the AWS console, 2) The user enter in their active directory single sign on credentials in to AWS, 3) The user's web browser receives a SAML assertion from AWS, 4) The user is then able to access the AWS Console.
B: 1) The user navigates to ADFS webserver, 2) The user enter in their single sign on credentials, 3) The user's web browser receives a SAML assertion from the AD server, 4) The user's browser then posts the SAML assertion to the AWS SAML end point for SAML and the AssumeRoleWithSAML API request is used to request temporary security credentials. 5) The user is then able to access the AWS Console.
C: 1) The user navigates to ADFS webserver, 2) The user enter in their single sign on credentials, 3) The user's web browser receives a SAML assertion from the AD server, 4) The user's browser then posts the SAML assertion to the AWS SAML end point for SAML and the GiveUserSAMLAccess API request is used to request temporary security credentials. 5) The user is then able to access the AWS Console.
D: Federating with Active Directory is not possible with AWS.




scroll down for answers:

 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
 |
\|/
 











## Answears
1-D, 2-C, 3-C, 4-B

