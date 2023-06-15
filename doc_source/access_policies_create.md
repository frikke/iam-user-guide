# Creating IAM policies<a name="access_policies_create"></a>

A [policy](access_policies.md) is an entity that, when attached to an identity or resource, defines their permissions\. You can use the AWS Management Console, AWS CLI, or AWS API to create *customer managed policies* in IAM\. Customer managed policies are standalone policies that you administer in your own AWS account\. You can then attach the policies to identities \(users, groups, and roles\) in your AWS account\.

A policy that is attached to an identity in IAM is known as an *identity\-based policy*\. Identity\-based policies can include AWS managed policies, customer managed policies, and inline policies\. AWS managed policies are created and managed by AWS\. You can use them, but you can't manage them\. An inline policy is one that you create and embed directly to an IAM group, user, or role\. Inline policies can't be reused on other identities or managed outside of the identity where it exists\. For more information, see [Adding and removing IAM identity permissions](access_policies_manage-attach-detach.md)\.

Use customer managed policies instead of inline policies\. It's also best to use customer managed policies instead of AWS managed policies\. AWS managed policies usually provide broad administrative or read\-only permissions\. For greatest security, [grant least privilege](best-practices.md#grant-least-privilege), which is granting only the permissions required to perform specific job tasks\.

When you create or edit IAM policies, AWS can automatically perform policy validation to help you create an effective policy with least privilege in mind\. In the AWS Management Console, IAM identifies JSON syntax errors, while IAM Access Analyzer provides additional policy checks with recommendations to help you further refine your policies\. To learn more about policy validation, see [Validating IAM policies](access_policies_policy-validator.md)\. To learn more about IAM Access Analyzer policy checks and actionable recommendations, see [ IAM Access Analyzer policy validation](https://docs.aws.amazon.com/IAM/latest/UserGuide/access-analyzer-policy-validation.html)\.

You can use the AWS Management Console, AWS CLI, or AWS API to create customer managed policies in IAM\. For more information about using AWS CloudFormation templates to add or update policies, see [AWS Identity and Access Management resource type reference](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/AWS_IAM.html) in the *AWS CloudFormation User Guide*\.

**Topics**
+ [Creating IAM policies \(console\)](access_policies_create-console.md)
+ [Creating IAM policies \(AWS CLI\)](access_policies_create-cli.md)
+ [Creating IAM policies \(AWS API\)](access_policies_create-api.md)