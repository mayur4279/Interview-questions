# AWS Identity and Access Management (IAM)

### 1. How do you control access to AWS services and resources using IAM?__

Create IAM users and assign policies as per requirement. This is how we can control the access of AWS services and resources.  

---

## 2. Explain the difference between an AWS user, group, role, and policy.

**AWS User:** An identity representing a person or service interacting with AWS resources. 

**AWS Group:** A collection of users. Different policies can be assigned to different groups.

**AWS Role:** Temporary access to users and services without the need for credentials, avoiding security issues. 

**Policy:** Permissions attached to roles, users, and groups.  
- **Types of Policies:**
  - AWS Managed Policy  
  - Custom Managed Policy 
  - Inline Policy  

---

## 3. What are the best practices for creating and managing IAM users in AWS?

1. Set a custom password policy for IAM users using the root account (strong password policy).
   - IAM service → Account settings → Edit → Custom.
2. Use auto-generated passwords whenever possible to enhance security.
3. Create groups for managing multiple IAM users.
4. Attach only the required policies to users or groups.
   - For example: A developer may only need access to the EC2 service for writing code.  

---

## 4. How do you enable multi-factor authentication (MFA) for AWS IAM users?

1. Go to IAM service.
2. Select the user.
3. Navigate to Security credentials.
4. Assign an MFA device.

---

## 5. Describe the process of setting up cross-account access in AWS IAM.


                Source account           --->          target account 
                                   wants to access        


1. **Create two IAM users known as  source account && target account**
   
   - **Target Account credentials**
   - https://975050134708.signin.aws.amazon.com/console  
   - target-account  
   - Mayur@4279  
   - **&& Assign All Administrator access policy.**

   <br> 

   - **Source account credentials**
   - https://975050134708.signin.aws.amazon.com/console
   - source-account 
   - Mayur@4279     
   - **&& only Assign  {awscloudshellfullaccess } policy.  --> for testing perpose**

2. Create an IAM Role in the Target Account

   - Sign in to the AWS Management Console in the target account.
   - Navigate to the IAM console.
   - Create a New Role.
     - Go to the "Roles" section and click on "Create role".
     - Select "Another AWS account" as the type of trusted entity.
   - Specify the Trusted Accounts
     - Enter the account ID (In this case select for this Aws account)
   - Attach Policies to the Role
     - Choose the permissions you want to grant to the role.
     - You can select AWS managed policies or create a custom policy.
     - For example, to allow full access to ec2, attach ec2FullAccess policy.
   - Complete the Role Creation
     - Provide a name and description for the role. - Review and create the role.
    

3. Assign STS Inline policy for source account.  (Using root account ) 

   -	Select the source account 
   -	In permission click on Add permission 
   -	Select create inline policy 
   -	Select service = STS  
   -	Click on ALL STS actions  && click on all resources 
   -	Give name and create the policy 

4. Navigate to source account and open cloudshell
   - In the source account, use the AWS STS `AssumeRole` API to get temporary credentials for the target account.
   - use following command
   <br>

   ```bash
   aws sts assume-role --role-arn arn:aws:iam::975050134708:role/ec2fullaccess --role-session-name mysession
   ```


   - results
     <p align="center">
     <img src="https://github.com/user-attachments/assets/4b073ed1-bcd5-4357-97b1-0aaa5504ede3" width="800" title="Architecture" alt="Architecture">
     </p>
  

5. for graphically access...

   Click on profile --> switch role  --> enter account Id  --> role name --> click on switch role.

     <p align="center">
     <img src="https://github.com/user-attachments/assets/97352231-756f-43a6-84ac-11620d0b2554" width="600" title="Architecture" alt="Architecture">
     </p>

     <p align="center">
     <img src="https://github.com/user-attachments/assets/a5292290-1666-4586-ae79-96228dc0c71a" width="400" title="Architecture" alt="Architecture">
     </p>

**Note: Now we can Access  ec2service using source account with the help of target account** 

---


## 6. What is AWS Identity Federation, and how does it work with IAM?

AWS Identity Federation allows users to access AWS resources using external identity providers (IdPs) like Google, Facebook, or corporate directories. It works by using the IdP to authenticate users and then providing them with temporary AWS credentials via AWS STS.

---

## 7. Explain the differences between IAM policies and resource-based policies in AWS.

**IAM Policies:** Policies attached directly to users, groups, and roles.

**Resource-based Policies:** Policies attached directly to resources such as EC2 instances or S3 buckets.

---

## 8. How do you rotate access keys for IAM users, and why is key rotation important?

1. Create a new access key.
2. Update code and configurations with the new access key.
3. Verify that all code is functioning properly.
4. Deactivate the old access key.
5. Delete the old access key.

Key rotation is important to reduce the risk of compromised credentials and maintain security best practices.

---

## 9. What is AWS Cognito, and how does it relate to IAM in the context of user identity and authentication?

AWS Cognito is a service that provides authentication, authorization, and user management for web and mobile applications. It helps in managing user pools and identity pools, and integrates with IAM to control access to AWS resources.

---

## 10. Explain the concept of AWS Security Token Service (STS) and how it relates to temporary credentials in IAM.

AWS STS is a service used for requesting  temporary credentials for AWS IAM users. 
These credentials are used to securely access AWS resources for a limited time.

For more details refer 5th question.. 

---

## 11. What are the limits for managed or custom managed policies and inline policies?

**Managed or Custom Managed Policies:** Up to 10 managed policies can be attached to a user, group, or role.

**Inline Policies:**  We can attach unlimited, no limit on this.  

---

## 12. What is a trusted entity in AWS?

we can Assign the roles to the trusted entities like aws account, services && IAM users.  
Trusted entities are defined in the trust policy attached to the IAM role.

Assume role :- "Assume Role" in AWS means allowing one entity (like a user, service, or another AWS account) to temporarily take on the permissions of a different IAM role.

---

## 13. Can you provide an example of a complex IAM scenario you've encountered in AWS and how you resolved it?

**I created s3 bucket and gave access to only one user using inline policy**

1. bucket is created using root account ( and put acl's disable and public access also disabled ) 
2. created a inline policy for normal IAM user using following json code.
   
   ```json
   {
	"Version": "2012-10-17",
	"Statement": [
		{
			"Sid": "VisualEditor0",
			"Effect": "Allow",
			"Action": [
				"s3:ListTagsForResource",
				"s3:ListBucketMultipartUploads",
				"s3:ListAccessGrants",
				"s3:ListBucketVersions",
				"s3:ListBucket",
				"s3:ListAccessGrantsLocations",
				"s3:ListMultipartUploadParts"
			],
			"Resource": "arn:aws:s3:::mayurs3bucketnamedddboyyyyy"
		},
		{
			"Sid": "VisualEditor1",
			"Effect": "Allow",
			"Action": [
				"s3:ListStorageLensConfigurations",
				"s3:ListAccessPointsForObjectLambda",
				"s3:ListAllMyBuckets",
				"s3:ListAccessPoints",
				"s3:ListAccessGrantsInstances",
				"s3:ListJobs",
				"s3:ListMultiRegionAccessPoints",
				"s3:ListStorageLensGroups"
			],
			"Resource": "*"
		}
	 ]
    }
   ```  

4. Now the IAM user only see the content of "mayurs3bucketnamedddboyyyyy" bucket.

     <p align="center">
     <img src="https://github.com/user-attachments/assets/5c7c98bf-0396-44da-8bc6-ca26c014a378" width="800" title="Architecture" alt="Architecture">
     </p>


---

## 14. Your organization is concerned about security breaches due to compromised AWS access keys. How would you implement a secure access key rotation strategy for IAM users?

1. Create new access keys.
2. Update applications and scripts to use the new keys.
3. Test thoroughly to ensure everything works with the new keys.
4. Deactivate the old keys.
5. Delete the old keys.

Additionally, enforce MFA and implement logging and monitoring to detect any unauthorized access attempts.

---

## 15. Your organization is migrating on-premises applications to AWS. How would you ensure a seamless transition for user authentication and authorization using AWS IAM?


1. first, i will create users
2. Second, i will create seperate groups for the users. 
3. third, based on exiting on-primises roles i will assign them policies such as for the group of developers i will only give the access of ec2 service.  
4. monitoration of all users using cloudtrail.  
---

## 16. Your organization has adopted AWS Organizations to manage multiple AWS accounts. How would you enforce IAM best practices and policies across these accounts efficiently?


1. Create seperate Centralize IAM management for service.
2. Add new policies day by day. 
3. Our organization use  AWS CloudTrail for continuous monitoring and compliance checks.

---
