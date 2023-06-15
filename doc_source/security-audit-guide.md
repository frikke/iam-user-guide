# AWS security audit guidelines<a name="security-audit-guide"></a>

Periodically audit your security configuration to make sure it meets your current business needs\. An audit gives you an opportunity to remove unneeded IAM users, roles, groups, and policies, and to make sure that your users and software don't have excessive permissions\. 

Following are guidelines for systematically reviewing and monitoring your AWS resources for security best practices\.

**Tip**  
You can monitor your usage of IAM as it relates to security best practices by using [AWS Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html)\. Security Hub uses security controls to evaluate resource configurations and security standards to help you comply with various compliance frameworks\. For more information about using Security Hub to evaluate IAM resources, see [AWS Identity and Access Management controls](https://docs.aws.amazon.com/securityhub/latest/userguide/iam-controls.html) in the AWS Security Hub User Guide\.

**Topics**
+ [When to perform a security audit](#security-audit-guide-when-to-audit)
+ [Guidelines for auditing](#security-audit-general-guidelines)
+ [Review your AWS account credentials](#security-audit-review-account)
+ [Review your IAM users](#security-audit-review-users)
+ [Review your IAM groups](#security-audit-groups)
+ [Review your IAM roles](#security-audit-review-roles)
+ [Review your IAM providers for SAML and OpenID Connect \(OIDC\)](#security-audit-review-saml-providers)
+ [Review Your mobile apps](#security-audit-review-mobile-apps)
+ [Tips for reviewing IAM policies](#security-audit-review-policy-tips)

## When to perform a security audit<a name="security-audit-guide-when-to-audit"></a>

Audit your security configuration in the following situations:
+ On a periodic basis\. Perform the steps described in this document at regular intervals as a best practice for security\.
+ If there are changes in your organization, such as people leaving\.
+ If you have stopped using one or more individual AWS services to verify that you have removed permissions that users in your account no longer need\.
+ If you've added or removed software in your accounts, such as applications on Amazon EC2 instances, AWS OpsWorks stacks, AWS CloudFormation templates, etc\.
+ If you suspect that an unauthorized person might have accessed your account\.

## Guidelines for auditing<a name="security-audit-general-guidelines"></a>

As you review your account's security configuration, follow these guidelines:
+ **Be thorough**\. Look at all aspects of your security configuration, including those that are seldom used\.
+ **Don't assume**\. If you are unfamiliar with some aspect of your security configuration \(for example, the reasoning behind a particular policy or the existence of a role\), investigate the business need until you understand the potential risk\.
+ **Keep things simple**\. To make auditing \(and management\) easier, use IAM groups, IAM roles, consistent naming schemes, and straightforward policies\.

## Review your AWS account credentials<a name="security-audit-review-account"></a>

Take these steps when you audit your AWS account credentials:

1. If you have access keys for your root user that you're not using, you can remove them\. We [strongly recommend](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html#root-password) that you don't use root access keys for everyday work with AWS, and that instead you use users with temporary credentials, such users in AWS IAM Identity Center \(successor to AWS Single Sign\-On\)\.

1. If you require access keys for your account, [rotate them regularly](https://docs.aws.amazon.com/IAM/latest/UserGuide/ManagingCredentials.html#Using_RotateAccessKey)\.

## Review your IAM users<a name="security-audit-review-users"></a>

Take these steps when you audit your existing IAM users:

1. [List your users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_manage.html#id_users_manage_list) and then [delete users](https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_DeletingUserFromAccount.html) that aren't needed\.

1.  [Remove users from groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_AddOrRemoveUsersFromGroup.html) that they don't require access to\.

1. Review the policies attached to the groups the user is in\. See [Tips for reviewing IAM policies](#security-audit-review-policy-tips)\.

1. Delete security credentials that the user doesn't need or that might have been exposed\. For example, an IAM user used for an application doesn't need a password \(which is necessary only to sign in to AWS websites\)\. Similarly, if a user doesn't use access keys, there's no reason for the user to have one\. For more information, see [Managing Passwords for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/credentials-add-pwd-for-user.html) and [Managing Access Keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/ManagingCredentials.html)\.

   You can generate and download a credential report that lists all IAM users in your account and the status of their various credentials, including passwords, access keys, and MFA devices\. For passwords and access keys, the credential report shows the date and time when the password or access key was last used\. Consider removing credentials that haven't been used recently from your account\. \(Don't remove your Emergency Access user\.\) For more information, see [Getting Credential Reports for your AWS Account](https://docs.aws.amazon.com/IAM/latest/UserGuide/credential-reports.html)\.

1. Rotate access keys regularly for use cases that require long\-term credentials\. For more information, see [Managing Passwords for IAM Users](https://docs.aws.amazon.com/IAM/latest/UserGuide/credentials-add-pwd-for-user.html) and [Managing Access Keys for IAM users](https://docs.aws.amazon.com/IAM/latest/UserGuide/ManagingCredentials.html)\.

1. As a best practice, require human users to use federation with an identity provider to access AWS using temporary credentials\. If possible, transition from IAM users to federated users, such as users in IAM Identity Center\. Retain the minimum number of IAM users needed for your applications\.

## Review your IAM groups<a name="security-audit-groups"></a>

Take these steps when you audit your IAM groups:

1. [List your groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups_manage_list.html) and then [delete groups](https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_DeleteGroup.html) that you aren't using\.

1. [Review users](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_manage.html#id_users_manage_list) in each group and [remove users](https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_AddOrRemoveUsersFromGroup.html) that don't belong\.

1. Review the policies attached to the group\. See [Tips for reviewing IAM policies](#security-audit-review-policy-tips)\. 

## Review your IAM roles<a name="security-audit-review-roles"></a>

Take these steps when you audit your IAM roles:

1. [List your roles](https://docs.aws.amazon.com/cli/latest/reference/iam/list-roles.html) and then [delete roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/roles-managingrole-deleting.html) that you aren't using\.

1. [Review](https://docs.aws.amazon.com/IAM/latest/UserGuide/roles-managingrole-editing.html) the role's trust policy\. Make sure that you know who the principal is and that you understand why that account or user needs to be able to assume the role\. 

1. [Review](https://docs.aws.amazon.com/IAM/latest/UserGuide/roles-managingrole-editing.html) the access policy for the role to be sure that it grants suitable permissions to whoever assumes the role—see [Tips for reviewing IAM policies](#security-audit-review-policy-tips)\. 

## Review your IAM providers for SAML and OpenID Connect \(OIDC\)<a name="security-audit-review-saml-providers"></a>

If you have created an IAM entity for establishing trust with a [SAML or OIDC identity provider \(IdP\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/identity-providers.html), take these steps:

1. Delete unused providers\. 

1. Download and review the AWS metadata documents for each SAML IdP and make sure the documents reflect your current business needs\. 

1. Get the latest metadata documents from the SAML IdPs and [update the provider in IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/identity-providers-saml.html)\. 

## Review Your mobile apps<a name="security-audit-review-mobile-apps"></a>

If you have created a mobile app that makes requests to AWS, take these steps:

1. Make sure that the mobile app doesn't contain embedded access keys, even if they're in encrypted storage\. 

1. Get temporary credentials for the app by using APIs designed for that purpose\.

**Note**  
We recommend that you use [Amazon Cognito](https://aws.amazon.com/cognito/) to manage user identity in your app\. This service lets you authenticate users using Login with Amazon, Facebook, Google, or any OpenID Connect \(OIDC\)–compatible identity provider\. For more information, see [Amazon Cognito identity pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-identity.html) in the *Amazon Cognito Developer Guide*\.

## Tips for reviewing IAM policies<a name="security-audit-review-policy-tips"></a>

Policies are powerful and subtle, so it's important to study and understand the permissions granted by each policy\. Use the following guidelines when reviewing policies: 
+ Attach policies to groups or roles instead of to individual users\. If an individual user has a policy, make sure you understand why that user needs the policy\.
+ Make sure that IAM users, groups, and roles have the permissions that they need and don't have any additional permissions\.
+ Use the [IAM Policy Simulator](https://docs.aws.amazon.com/IAM/latest/UsingPolicySimulatorGuide/) to test policies attached to users or groups\.
+ Remember that a user's permissions are the result of all applicable policies— both identity\-based policies \(on users, groups,or roles\) and resource\-based policies \(on resources such as Amazon S3 buckets, Amazon SQS queues, Amazon SNS topics, and AWS KMS keys\)\. It's important to examine all the policies that apply to a user and to understand the complete set of permissions granted to an individual user\.
+ Be aware that allowing a user to create an IAM user, group, role, or policy and attach a policy to the principal entity is effectively granting that user all permissions to all resources in your account\. Users who can create policies and attach them to a user, group, or role can grant themselves any permissions\. In general, don't grant IAM permissions to users or roles whom you don't trust with full access to the resources in your account\. When conducting your security audit confirm that the following IAM permissions are granted to trusted identities: 
  + `iam:PutGroupPolicy`
  + `iam:PutRolePolicy`
  + `iam:PutUserPolicy`
  + `iam:CreatePolicy`
  + `iam:CreatePolicyVersion`
  + `iam:AttachGroupPolicy`
  + `iam:AttachRolePolicy`
  + `iam:AttachUserPolicy`
+ Make sure policies don't grant permissions for services that you don't use\. For example, if you use [AWS managed policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/policies-managed-vs-inline.html#aws-managed-policies), make sure the AWS managed policies that are in use in your account are for services that you actually use\. To find out which AWS managed policies are in use in your account, use the IAM [https://docs.aws.amazon.com/IAM/latest/APIReference/API_GetAccountAuthorizationDetails.html](https://docs.aws.amazon.com/IAM/latest/APIReference/API_GetAccountAuthorizationDetails.html) API \(AWS CLI command: [https://docs.aws.amazon.com/cli/latest/reference/iam/get-account-authorization-details.html](https://docs.aws.amazon.com/cli/latest/reference/iam/get-account-authorization-details.html)\)\.
+ If the policy grants a user permission to launch an Amazon EC2 instance, it might also allow the `iam:PassRole` action, but if so it should [explicitly list the roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/roles-usingrole-ec2instance.html#roles-usingrole-ec2instance-passrole) that the user can pass to the Amazon EC2 instance\. 
+ Examine any values for the `Action` or `Resource` element that include `*`\. When possible, grant `Allow` access to the individual actions and resources that users need\. However, the following are reasons that it might be suitable to use `*` in a policy:
  + The policy is designed to grant administrative\-level permissions\.
  + The wildcard character is used for a set of similar actions \(for example, `Describe*`\) as a convenience, and you are comfortable with the complete list of actions that are referenced in this way\.
  + The wildcard character is used to indicate a class of resources or a resource path \(for example, `arn:aws:iam::account-id:users/division_abc/*`\), and you are comfortable granting access to all the resources in that class or path\.
  + A service action doesn't support resource\-level permissions, and the only choice for a resource is `*`\.
+ Examine policy names to make sure they reflect the policy's function\. For example, although a policy might have a name that includes "read only," the policy might actually grant write or change permissions\.

For more information about planning for your security audit, see [Best Practices for Security, Identity, and Compliance](http://aws.amazon.com/architecture/security-identity-compliance/) in the *AWS Architecture Center*\.