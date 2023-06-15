# AWS account root user<a name="id_root-user"></a>

When you first create an Amazon Web Services \(AWS\) account, you begin with a single sign\-in identity that has complete access to all AWS services and resources in the account\. This identity is called the AWS account *root user* and is accessed by signing in with the email address and password that you used to create the account\.

We strongly recommend that you do not use the root user for your everyday tasks, even the administrative ones\. As a [best practice](best-practices.md), safeguard your root user credentials and don't use them for everyday tasks\. Root user credentials are only used to perform a few account and service management tasks\.

 To view the tasks that require you to sign in as the root user, see [Tasks that require root user credentials](https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html)\.

You can create, rotate, disable, or delete access keys \(access key IDs and secret access keys\) for your AWS account root user\. You can also change your root user password\. Anyone who has root user credentials for your AWS account has unrestricted access to all the resources in your account, including billing information\.

When you create access keys, you create the access key ID and secret access key as a set\. During access key creation, AWS gives you one opportunity to view and download the secret access key part of the access key\. If you don't download it or if you lose it, you can delete the access key and then create a new one\. You can create root user access keys with the [IAM console](https://console.aws.amazon.com/iam/home?#), AWS CLI, or AWS API\.

A newly created access key has the status of *active*, which means that you can use the access key for CLI and API calls\. You are [limited to two access keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_iam-quotas.html) for each IAM user, which is useful when you want to [rotate the access keys](https://docs.aws.amazon.com/general/latest/gr/aws-access-keys-best-practices.html#iam-user-access-keys)\. You can also assign up to two access keys to the root user\. When you disable an access key, you can't use it for API calls\. Inactive keys still count toward your limit\. You can create or delete an access key any time\. However, when you delete an access key, it's gone forever and can't be retrieved\.

You can change the email address and password on the [Security Credentials](https://console.aws.amazon.com/iam/home?#security_credential) page\. You can also choose **Forgot password?** on the AWS sign\-in page to reset your password\.

**Topics**
+ [Create or delete an AWS account](#id_root-user_manage_account)
+ [Enable MFA on the AWS account root user](#id_root-user_manage_mfa)
+ [Creating access keys for the root user](#id_root-user_manage_add-key)
+ [Deleting access keys for the root user](#id_root-user_manage_delete-key)
+ [Changing the password for the root user](#id_root-user_manage_password)
+ [Securing the credentials for the root user](#id_root-user_secure_credentials)
+ [Transferring the root user owner](#id_root-user_transfer_account)

## Create or delete an AWS account<a name="id_root-user_manage_account"></a>

For more information, see the following articles in the AWS Knowledge Center:
+ [How do I create and activate an AWS account?](http://aws.amazon.com/premiumsupport/knowledge-center/create-and-activate-aws-account/)
+ [How do I close my AWS account?](http://aws.amazon.com/premiumsupport/knowledge-center/close-aws-account/)

## Enable MFA on the AWS account root user<a name="id_root-user_manage_mfa"></a>

We recommend that you follow the security best practice to enable multi\-factor authentication \(MFA\) for your account\. Because your root user can perform sensitive operations in your account, adding an additional layer of authentication helps you to better secure your account\. Multiple types of MFA are available\. We recommend that you enable multiple MFA devices to your AWS account root user and IAM users in your AWS accounts\. This allows you to raise the security bar in your AWS accounts, including your AWS account root user\. You can register up to eight MFA devices of any combination of the currently supported MFA types for your AWS account root user and IAM users\.

With multiple MFA devices, only one MFA device is needed to sign in to the AWS Management Console or create a session using the AWS CLI as that user\. For more information, see [How do I use an MFA token to authenticate access to my AWS resources through the AWS CLI?](https://aws.amazon.com/premiumsupport/knowledge-center/authenticate-mfa-cli/)

 For more information about enabling MFA, see the following:
+ [Enable a virtual MFA device for your AWS account root user \(console\)](id_credentials_mfa_enable_virtual.md#enable-virt-mfa-for-root)
+ [Enable a hardware TOTP token for the AWS account root user \(console\)](id_credentials_mfa_enable_physical.md#enable-hw-mfa-for-root)

## Creating access keys for the root user<a name="id_root-user_manage_add-key"></a>

Although we don't recommend it, you can use the AWS Management Console or AWS programming tools to create access keys for the root user\.

**To create an access key for the AWS account root user \(console\)**

1. Sign in to the [IAM console](https://console.aws.amazon.com/iam/) as the account owner by choosing **Root user** and entering your AWS account email address\. On the next page, enter your password\.
**Note**  
As the root user, you can't sign in to the **Sign in as IAM user** page\. If you see the **Sign in as IAM user** page, choose **Sign in using root user email** near the bottom of the page\. For help signing in as the root user, see [Signing in to the AWS Management Console as the root user](https://docs.aws.amazon.com/signin/latest/userguide/introduction-to-          root-user-sign-in-tutorial.html) in the *AWS Sign\-In User Guide*\.

1. Choose your account name in the navigation bar, and then choose **Security credentials**\. 

1. If you see a warning about accessing the security credentials for your AWS account, choose **Continue to Security credentials**\.

1. Review the alternatives\. We don't recommend that you create root user access keys\. If you choose to continue to create an access key, select the check box to indicate that you understand that this is not a best practice, and then choose **Create access key**\.

1. On the **Retrieve access key** page, choose either **Show** or **Download \.csv file**\. This is your only opportunity to save your secret access key\. After you've saved your secret access key in a secure location, chose **Done**\.

   If you choose **Download \.csv file**, you receive a file named `rootkey.csv` that contains the access key ID and the secret key\. Save the file somewhere safe\.

1. When you no longer use the access key [we recommend that you delete it](best-practices.md#remove-credentials), or at least deactivate it by choosing **Actions** and then **Deactivate** so that it cannot be misused\.

**To create an access key for the root user \(AWS CLI or AWS API\)**

Use one of the following:
+ AWS CLI: [aws iam create\-access\-key](https://docs.aws.amazon.com/cli/latest/reference/iam/create-access-key.html)
+ AWS API: [CreateAccessKey](https://docs.aws.amazon.com/IAM/latest/APIReference/API_CreateAccessKey.html) 

## Deleting access keys for the root user<a name="id_root-user_manage_delete-key"></a>

You can use the AWS Management Console to delete access keys for the root user\.

1. Use your AWS account email address and password to sign in to the [AWS Management Console](https://console.aws.amazon.com/) as the AWS account root user\.
**Note**  
If you see three text boxes, then you previously signed in to the console with *[IAM user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users.html)* credentials\. Your browser might remember this preference and open this account\-specific sign\-in page every time that you try to sign in\. You cannot use the IAM user sign\-in page to sign in as the account owner\. If you see the [IAM user sign\-in page](https://docs.aws.amazon.com/IAM/latest/UserGuide/console.html#user-sign-in-page), choose **Sign in using root user email** near the bottom of the page\. This returns you to the main sign\-in page\. From there, you can sign in as the root user using your AWS account email address and password\.

1. Choose your account name in the navigation bar, and then choose **Security credentials**\. 

1. If you see a warning about accessing the security credentials for your AWS account, choose **Continue to Security credentials**\.

1. On the next screen, choose **Deactivate**\. This deactivates the access key\. We recommend that you verify that the access key is no longer in use before you permanently delete it\. To confirm deletion, copy the access key ID, paste the access key ID in the text input field, and then choose **Delete**\.

## Changing the password for the root user<a name="id_root-user_manage_password"></a>

For information about changing the password for the root user, see [Changing the AWS account root user password](id_credentials_passwords_change-root.md)\. To change the root user, you must log in using the root user credentials\. For the complete list of tasks that require you to sign in as the root user, see [Tasks that require root user credentials](https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html) in the *AWS Account Management Reference Guide*\. \.

## Securing the credentials for the root user<a name="id_root-user_secure_credentials"></a>

For more information about securing the credentials for the AWS account root user, see [Safeguard your root user credentials and don't use them for everyday tasks](best-practices.md#lock-away-credentials)\.

## Transferring the root user owner<a name="id_root-user_transfer_account"></a>

To transfer ownership of the root user, see [How do I transfer my AWS account to another person or business?](https://aws.amazon.com/premiumsupport/knowledge-center/transfer-aws-account/)\. 