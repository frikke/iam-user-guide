# IAM user groups<a name="id_groups"></a>

An IAM [*user group*](#id_groups) is a collection of IAM users\. User groups let you specify permissions for multiple users, which can make it easier to manage the permissions for those users\. For example, you could have a user group called *Admins* and give that user group typical administrator permissions\. Any user in that user group automatically has *Admins* group permissions\. If a new user joins your organization and needs administrator privileges you can assign the appropriate permissions by adding the user to the *Admins* user group\. If a person changes jobs in your organization, instead of editing that user's permissions you can remove them from the old user groups and add them to the appropriate new user groups\. 

You can attach an identity\-based policy to a user group so that all of the users in the user group receive the policy's permissions\. You cannot identify a user group as a `Principal` in a policy \(such as a resource\-based policy\) because groups relate to permissions, not authentication, and principals are authenticated IAM entities\. For more information about policy types, see [Identity\-based policies and resource\-based policies](access_policies_identity-vs-resource.md)\.

Here are some important characteristics of user groups:
+ A user group can contain many users, and a user can belong to multiple user groups\.
+ User groups can't be nested; they can contain only users, not other user groups\.
+ There is no default user group that automatically includes all users in the AWS account\. If you want to have a user group like that, you must create it and assign each new user to it\.
+ The number and size of IAM resources in an AWS account, such as the number of groups, and the number of groups that a user can be a member of, are limited\. For more information, see [IAM and AWS STS quotas, name requirements, and character limits](reference_iam-quotas.md)\.

The following diagram shows a simple example of a small company\. The company owner creates an `Admins` user group for users to create and manage other users as the company grows\. The `Admins` user group creates a `Developers` user group and a `Test` user group\. Each of these user groups consists of users \(humans and applications\) that interact with AWS \(Jim, Brad, DevApp1, and so on\)\. Each user has an individual set of security credentials\. In this example, each user belongs to a single user group\. However, users can belong to multiple user groups\.

![\[Example of relationship between AWS accounts, users, and user groups\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/Relationship_Between_Entities_Example.diagram.png)