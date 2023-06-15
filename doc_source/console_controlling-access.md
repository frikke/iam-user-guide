# Controlling IAM users access to the AWS Management Console<a name="console_controlling-access"></a>

IAM users with permission who sign in to your AWS account through the AWS Management Console can access your AWS resources\. The following list shows the ways that you can grant IAM users access to your AWS account resources through the AWS Management Console\. It also shows how IAM users can access other AWS account features through the AWS website\.

**Note**  
There is no charge to use IAM\.

**The AWS Management Console**  
You create a password for each IAM user who needs access to the AWS Management Console\. Users access the console through your IAM\-enabled AWS account sign\-in page\. For information about accessing the sign\-in page, see [How to sign in to AWS](https://docs.aws.amazon.com/signin/latest/userguide/how-to-sign-in.html) in the *AWS Sign\-In User Guide*\. For information about creating passwords, see [Managing user passwords in AWS](id_credentials_passwords.md)\.  
You can prevent an IAM user from accessing the AWS Management Console by removing their password\. This prevents them from signing into the AWS Management Console using their sign\-in credentials\. It does not change their permissions or prevent them from accessing the console using an assumed role\. If the user has active access keys, they continue to function and allow access through the AWS CLI, Tools for Windows PowerShell, AWS API, or the AWS Console Mobile Application\.

**Your AWS resources, such as Amazon EC2 instances, Amazon S3 buckets, and so on**  
Even if your IAM users have passwords, they still need permission to access your AWS resources\. When you create an IAM user, that user has no permissions by default\. To give your IAM users the permissions they need, you attach policies to them\. If you have many IAM users who perform the same tasks with the same resources, you can assign those IAM users to a group\. Then assign the permissions to that group\. For information about creating IAM users and groups, see [IAM Identities \(users, user groups, and roles\)](id.md)\. For information about using policies to set permissions, see [Access management for AWS resources](access.md)\.

**AWS Discussion Forums**  
Anyone can read the posts on the [AWS Discussion Forums](https://forums.aws.amazon.com/)\. Users who want to post questions or comments to the AWS Discussion Forum can do so using their user name\. The first time a user posts to the AWS Discussion Forum, the user is prompted to enter a nickname and email address\. Only that user can use that nickname in the AWS Discussion Forums\. 

**Your AWS account billing and usage information**  
You can grant users access your AWS account billing and usage information\. For more information, see [ Controlling Access to Your Billing Information](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/control-access-billing.html) in the *AWS Billing User Guide*\. 

**Your AWS account profile information**  
Users cannot access your AWS account profile information\.

**Your AWS account security credentials**  
Users cannot access your AWS account security credentials\.

**Note**  
IAM policies control access regardless of the interface\. For example, you could provide a user with a password to access the AWS Management Console\. The policies for that user \(or any groups the user belongs to\) would control what the user can do in the AWS Management Console\. Or, you could provide the user with AWS access keys for making API calls to AWS\. The policies would control which actions the user could call through a library or client that uses those access keys for authentication\.