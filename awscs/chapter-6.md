# 第六章 AWS Identity and Access Management (IAM)
**《AWS认证解决方案架构师-联合考试》中的本章节目标包括不限于如下内容：**

## Principals


## Authentication



## Authorization


## 其他的关键特性



## 总结


## 考试基础


## 练习




## 复习题

### 1. Which of the following methods will allow an application using an AWS SDK to be authenticated as a principal to access AWS Cloud services? (Choose 2 answers)
 * A. Create an IAM user and store the user name and password for the user in the application’s configuration.
 * B. Create an IAM user and store both parts of the access key for the user in the application’s configuration.
 * C. Run the application on an Amazon EC2 instance with an assigned IAM role.
 * D. Make all the API calls over an SSL connection.

### 2. Which of the following are found in an IAM policy? (Choose 2 answers)
 * A. Service Name
 * B. Region
 * C. Action
 * D. Password

### 3. Your AWS account administrator left your company today. The administrator had access to the root user and a personal IAM administrator account. With these accounts, he generated other IAM accounts and keys. Which of the following should you do today to protect your AWS infrastructure? (Choose 4 answers)
 * A. Change the password and add MFA to the root user.
 * B. Put an IP restriction on the root user.
 * C. Rotate keys and change passwords for IAM accounts.
 * D. Delete all IAM accounts.
 * E. Delete the administrator’s personal IAM account.
 * F. Relaunch all Amazon EC2 instances with new roles.

### 4. Which of the following actions can be authorized by IAM? (Choose 2 answers)
 * A. Installing ASP.NET on a Windows Server
 * B. Launching an Amazon Linux EC2 instance
 * C. Querying an Oracle database
 * D. Adding a message to an Amazon Simple Queue Service (Amazon SQS) queue

### 5. Which of the following are IAM security features? (Choose 2 answers)
 * A. Password policies
 * B. Amazon DynamoDB global secondary indexes
 * C. MFA
 * D. Consolidated Billing

### 6. Which of the following are benefits of using Amazon EC2 roles? (Choose 2 answers)
 * A. No policies are required.
 * B. Credentials do not need to be stored on the Amazon EC2 instance.
 * C. Key rotation is not necessary.
 * D. Integration with Active Directory is automatic.

### 7. Which of the following are based on temporary security tokens? (Choose 2 answers)
 * A. Amazon EC2 roles
 * B. MFA
 * C. Root user
 * D. Federation

### 8. Your security team is very concerned about the vulnerability of the IAM administrator user accounts (the accounts used to configure all IAM features and accounts). What steps can be taken to lock down these accounts? (Choose 3 answers)
 * A. Add multi-factor authentication (MFA) to the accounts.
 * B. Limit logins to a particular U.S. state.
 * C. Implement a password policy on the AWS account.
 * D. Apply a source IP address condition to the policy that only grants permissions when the user is on the corporate network.
 * E. Add a CAPTCHA test to the accounts.

### 9. You want to grant the individuals on your network team the ability to fully manipulate Amazon EC2 instances. Which of the following accomplish this goal? (Choose 2 answers)
 * A. Create a new policy allowing EC2:* actions, and name the policy NetworkTeam.
 * B. Assign the managed policy, EC2FullAccess, to a group named NetworkTeam, and assign all the team members’ IAM user accounts to that group.
 * C. Create a new policy that grants EC2:* actions on all resources, and assign that policy to each individual’s IAM user account on the network team.
 * D. Create a NetworkTeam IAM group, and have each team member log in to the AWS Management Console using the user name/password for the group.

### 10. What is the format of an IAM policy?
 * A. XML
 * B. Key/value pairs
 * C. JSON
 * D. Tab-delimited text