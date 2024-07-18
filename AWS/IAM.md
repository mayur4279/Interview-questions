# IAM

## 1. How do you control access to AWS services and resources using IAM?
   
Create IAM user and assign policies as per requirement. This is how we can control the access of AWS services and resources.  

---

## 2. Explain the difference between an AWS user, group, role, and policy.

**AWS user:** Aws user is an identity which represents a person or the service interacting with AWS resources. 

**AWS group:** Collection of users. We can assign different policies to different groups.

**AWS role:** Role is a Temporary access to user and services (without credentials to avoid security issues). 

**Policy:** Is a permission which we attach to the roles, users, and groups.  
- Two types:
  1. AWS managed policy  
  2. Custom managed policy 
  3. Inline policy  

---

## 3. What are the best practices for creating and managing IAM users in AWS?

1. Set a custom password policy for IAM user password using root account (strong password policy).
   - IAM service --> Account settings --> Edit --> custom.
2. If possible, use an auto-generated password because it is complex to crack for hackers.
3. Create groups for managing multiple IAM users.
4. Attach only required policies to users or groups.
   - For example: Developer only requires access to EC2 service for writing code.  

---

## 4. How do you enable multi-factor authentication (MFA) for AWS IAM users?

{ IAM service --> users --> select user --> Security credentials --> Assign MFA device } 

---

## 5. Describe the process of setting up cross-account access in AWS IAM.

---

## 6. What is AWS Identity Federation, and how does it work with IAM?

---

## 7. Explain the differences between IAM policies and resource-based policies in AWS.

**IAM policies:** Policy is directly attached to the users, groups, and roles.

**Resource-based policies:** Policy is directly attached to the resources like EC2, S3.

---

## 8. How do you rotate access keys for IAM users, and why is key rotation important?

1. Create new access key.
2. Update code and configuration with new access key.
3. Verify all the code is working properly.
4. Deactivate the access key.
5. Delete the old key.

---

## 9. What is AWS Cognito, and how does it relate to IAM in the context of user identity and authentication?

---

## 10. Explain the concept of AWS Security Token Service (STS) and how it relates to temporary credentials in IAM.

---

## 11. Limit managed or custom managed policies

---

## 12. What is a trusted entity in AWS?

---

## 13. Can you provide an example of a complex IAM scenario you've encountered in AWS and how you resolved it?

---

## 14. Your organization is concerned about security breaches due to compromised AWS access keys. How would you implement a secure access key rotation strategy for IAM users?

---

## 15. Your organization is migrating on-premises applications to AWS. How would you ensure a seamless transition for user authentication and authorization using AWS IAM?

---

## 16. Your organization has adopted AWS Organizations to manage multiple AWS accounts. How would you enforce IAM best practices and policies across these accounts efficiently?

---
