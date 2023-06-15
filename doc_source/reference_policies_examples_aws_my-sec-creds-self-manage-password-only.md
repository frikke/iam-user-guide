# AWS: Allows IAM users to change their own console password on the My security credentials page<a name="reference_policies_examples_aws_my-sec-creds-self-manage-password-only"></a>

This example shows how you might create an identity\-based policy that allows IAM users to change their own AWS Management Console password on the **My security credentials** page\. This AWS Management Console page displays account and user information, but the user can only access their own password\. To allow users to manage all of their own credentials with MFA, see [AWS: Allows MFA\-authenticated IAM users to manage their own credentials on the My security credentials page](reference_policies_examples_aws_my-sec-creds-self-manage.md)\. To allow users to manage their own credentials without using MFA, see [AWS: Allows IAM users to manage their own credentials on the My security credentials page](reference_policies_examples_aws_my-sec-creds-self-manage-no-mfa.md)\.

To learn how users can access the **My security credentials** page, see [How IAM users change their own password \(console\)](id_credentials_passwords_user-change-own.md#ManagingUserPwdSelf-Console)\.

**What does this policy do? **
+ The `ViewAccountPasswordRequirements` statement allows the user to view the account password requirements while changing their own IAM user password\.
+ The `ChangeOwnPassword` statement allows the user to change their own password\. This statement also includes the `GetUser` action, which is required to view most of the information on the **My security credentials** page\.

This policy does not allow users to view the **Users** page in the IAM console or use that page to access their own user information\. To allow this, add the `iam:ListUsers` action to the `ViewAccountPasswordRequirements` statement\. It also does not allow users to change their password on their own user page\. To allow this, add the `iam:GetLoginProfile` and `iam:UpdateLoginProfile` actions to the `ChangeOwnPasswords` statement\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ViewAccountPasswordRequirements",
            "Effect": "Allow",
            "Action": "iam:GetAccountPasswordPolicy",
            "Resource": "*"
        },
        {
            "Sid": "ChangeOwnPassword",
            "Effect": "Allow",
            "Action": [
                "iam:GetUser",
                "iam:ChangePassword"
            ],
            "Resource": "arn:aws:iam::*:user/${aws:username}"
        }
    ]
}
```