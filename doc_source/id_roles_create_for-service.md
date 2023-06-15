# Creating a role to delegate permissions to an AWS service<a name="id_roles_create_for-service"></a>

Many AWS services require that you use roles to allow the service to access resources in other services on your behalf\. A role that a service assumes to perform actions on your behalf is called a [service role](id_roles_terms-and-concepts.md#iam-term-service-role)\. When a role serves a specialized purpose for a service, it is categorized as a [service role for EC2 instances](id_roles_terms-and-concepts.md#iam-term-service-role-ec2) \(for example\), or a [service\-linked role](id_roles_terms-and-concepts.md#iam-term-service-linked-role)\. To see what services support using service\-linked roles, or whether a service supports any form of temporary credentials, see [AWS services that work with IAM](reference_aws-services-that-work-with-iam.md)\. To learn how an individual service uses roles, choose the service name in the table to view the documentation for that service\.

For information about how roles help you to delegate permissions, see [Roles terms and concepts](id_roles_terms-and-concepts.md)\.

## Service role permissions<a name="id_roles_create_service-permissions"></a>

You must configure permissions to allow an IAM entity \(user or role\) to create or edit a service role\.

**Note**  
The ARN for a service\-linked role includes a service principal, which is indicated in the following policies as `SERVICE-NAME.amazonaws.com`\. Do not try to guess the service principal, because it is case\-sensitive and the format can vary across AWS services\. To view the service principal for a service, see its service\-linked role documentation\.

**To allow an IAM entity to create a specific service role**

Add the following policy to the IAM entity that needs to create the service role\. This policy allows you to create a service role for the specified service and with a specific name\. You can then attach managed or inline policies to that role\. 

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:AttachRolePolicy",
                "iam:CreateRole",
                "iam:PutRolePolicy"
            ],
            "Resource": "arn:aws:iam::*:role/SERVICE-ROLE-NAME"
        }
    ]
}
```

**To allow an IAM entity to create any service role**

AWS recommends that you allow only administrative users to create any service role\. A person with permissions to create a role and attach any policy can escalate their own permissions\. Instead, create a policy that allows them to create only the roles that they need or have an administrator create the service role on their behalf\.

To attach a policy that allows an administrator to access your entire AWS account, use the [AdministratorAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AdministratorAccess) AWS managed policy\.

**To allow an IAM entity to edit a service role**

Add the following policy to the IAM entity that needs to edit the service role\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "EditSpecificServiceRole",
            "Effect": "Allow",
            "Action": [
                "iam:AttachRolePolicy",
                "iam:DeleteRolePolicy",
                "iam:DetachRolePolicy",
                "iam:GetRole",
                "iam:GetRolePolicy",
                "iam:ListAttachedRolePolicies",
                "iam:ListRolePolicies",
                "iam:PutRolePolicy",
                "iam:UpdateRole",
                "iam:UpdateRoleDescription"
            ],
            "Resource": "arn:aws:iam::*:role/SERVICE-ROLE-NAME"
        },
        {
            "Sid": "ViewRolesAndPolicies",
            "Effect": "Allow",
            "Action": [
                "iam:GetPolicy",
                "iam:ListRoles"
            ],
            "Resource": "*"
        }
    ]
}
```

**To allow an IAM entity to delete a specific service role**

Add the following statement to the permissions policy for the IAM entity that needs to delete the specified service role\.

```
{
    "Effect": "Allow",
    "Action": "iam:DeleteRole",
    "Resource": "arn:aws:iam::*:role/SERVICE-ROLE-NAME"
}
```

**To allow an IAM entity to delete any service role**

AWS recommends that you allow only administrative users to delete any service role\. Instead, create a policy that allows them to delete only the roles that they need or have an administrator delete the service role on their behalf\.

To attach a policy that allows an administrator to access your entire AWS account, use the [AdministratorAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AdministratorAccess) AWS managed policy\.

## Creating a role for an AWS service \(console\)<a name="roles-creatingrole-service-console"></a>

You can use the AWS Management Console to create a role for a service\. Because some services support more than one service role, see the [AWS documentation](https://docs.aws.amazon.com/) for your service to see which use case to choose\. You can learn how to assign the necessary trust and permissions policies to the role so that the service can assume the role on your behalf\. The steps that you can use to control the permissions for your role can vary, depending on how the service defines the use cases, and whether or not you create a service\-linked role\.

**To create a role for an AWS service \(console\)**

1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane of the IAM console, choose **Roles**, and then choose **Create role**\.

1. For **Select trusted entity**, choose **AWS service**\. 

1. Choose the use case for your service\. Use cases are defined by the service to include the trust policy required by the service\. Then, choose **Next**\.

1. If possible, select the policy to use for the permissions policy or choose **Create policy** to open a new browser tab and create a new policy from scratch\. For more information, see [Creating IAM policies](access_policies_create-console.md#access_policies_create-start)\. After you create the policy, close that tab and return to your original tab\. Select the check box next to the permissions policies that you want the service to have\.

   Depending on the use case that you selected, the service might allow you to do any of the following:
   + Nothing, because the service defines the permissions for the role\.
   + Choose from a limited set of permissions\.
   + Choose from any permissions\.
   + Select no policies at this time, create the policies later, and then attach them to the role\.

1. \(Optional\) Set a [permissions boundary](access_policies_boundaries.md)\. This is an advanced feature that is available for service roles, but not service\-linked roles\. 

   Expand the **Permissions boundary** section and choose **Use a permissions boundary to control the maximum role permissions**\. IAM includes a list of the AWS managed and customer managed policies in your account\. Select the policy to use for the permissions boundary, or choose **Create policy** to open a new browser tab and create a new policy from scratch\. For more information, see [Creating IAM policies](access_policies_create-console.md#access_policies_create-start)\. After you create the policy, close that tab and return to your original tab to select the policy to use for the permissions boundary\.

1. Choose **Next**\.

1. For **Role name**, the degree of role name customization is defined by the service\. If the service defines the role's name, this option is not editable\. In other cases, the service might define a prefix for the role and allow you to enter an optional suffix\. Some services allow you to specify the entire name of your role\.

   If possible, enter a role name or role name suffix to help you identify the purpose of this role\. Role names must be unique within your AWS account\. They are not distinguished by case\. For example, you cannot create roles named both **PRODROLE** and **prodrole**\. Because other AWS resources might reference the role, you cannot edit the name of the role after it has been created\.

1. \(Optional\) For **Description**, enter a description for the new role\.

1. Choose **Edit** in the **Step 1: Select trusted entities** or **Step 2: Add permissions** sections to edit the use cases and permissions for the role\. 

1. \(Optional\) Add metadata to the role by attaching tags as key–value pairs\. For more information about using tags in IAM, see [Tagging IAM resources](id_tags.md)\.

1. Review the role and then choose **Create role**\.

## Creating a role for a service \(AWS CLI\)<a name="roles-creatingrole-service-cli"></a>

Creating a role from the AWS CLI involves multiple steps\. When you use the console to create a role, many of the steps are done for you, but with the AWS CLI you must explicitly perform each step yourself\. You must create the role and then assign a permissions policy to the role\. If the service you are working with is Amazon EC2, then you must also create an instance profile and add the role to it\. Optionally, you can also set the [permissions boundary](access_policies_boundaries.md) for your role\.

**To create a role for an AWS service from the AWS CLI**

1. The following `[create\-role](https://docs.aws.amazon.com/cli/latest/reference/iam/create-role.html)` command creates a role named *Test\-Role* and attaches a trust policy to it:

   aws iam create\-role \-\-role\-name Test\-Role \-\-assume\-role\-policy\-document file://Test\-Role\-Trust\-Policy\.json

1. Attach a managed permissions policy to the role: [aws iam attach\-role\-policy](https://docs.aws.amazon.com/cli/latest/reference/iam/attach-role-policy.html)\.

   For example, the following `attach-role-policy` command attaches the AWS managed policy named `ReadOnlyAccess` to the IAM role named `ReadOnlyRole`:

   aws iam attach\-role\-policy \-\-policy\-arn arn:aws:iam::aws:policy/ReadOnlyAccess \-\-role\-name ReadOnlyRole

    or

   Create an inline permissions policy for the role: [aws iam put\-role\-policy](https://docs.aws.amazon.com/cli/latest/reference/iam/put-role-policy.html)

   To add an inline permissions policy, see the following example:

    aws iam put\-role\-policy \-\-role\-name Test\-Role \-\-policy\-name ExamplePolicy \-\-policy\-document file://AdminPolicy\.json

1. \(Optional\) Add custom attributes to the role by attaching tags: [aws iam tag\-role](https://docs.aws.amazon.com/cli/latest/reference/iam/tag-role.html)

   For more information, see [Managing tags on IAM roles \(AWS CLI or AWS API\)](id_tags_roles.md#id_tags_roles_procs-cli-api)\.

1. \(Optional\) Set the [permissions boundary](access_policies_boundaries.md) for the role: [aws iam put\-role\-permissions\-boundary](https://docs.aws.amazon.com/cli/latest/reference/iam/put-role-permissions-boundary.html)

   A permissions boundary controls the maximum permissions that a role can have\. Permissions boundaries are an advanced AWS feature\.

If you are going to use the role with Amazon EC2 or another AWS service that uses Amazon EC2, you must store the role in an instance profile\. An instance profile is a container for a role that can be attached to an Amazon EC2 instance when launched\. An instance profile can contain only one role, and that limit cannot be increased\. If you create the role using the AWS Management Console, the instance profile is created for you with the same name as the role\. For more information about instance profiles, see [Using instance profiles](id_roles_use_switch-role-ec2_instance-profiles.md)\. For information about how to launch an EC2 instance with a role, see [Controlling Access to Amazon EC2 Resources](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/UsingIAM.html#UsingIAMrolesWithAmazonEC2Instances) in the *Amazon EC2 User Guide for Linux Instances*\.

**To create an instance profile and store the role in it \(AWS CLI\)**

1. Create an instance profile: [aws iam create\-instance\-profile](https://docs.aws.amazon.com/cli/latest/reference/iam/create-instance-profile.html)

1. Add the role to the instance profile: [aws iam add\-role\-to\-instance\-profile](https://docs.aws.amazon.com/cli/latest/reference/iam/add-role-to-instance-profile.html)

The AWS CLI example command set below demonstrates the first two steps for creating a role and attaching permissions\. It also shows the two steps for creating an instance profile and adding the role to the profile\. This example trust policy allows the Amazon EC2 service to assume the role and view the `example_bucket` Amazon S3 bucket\. The example also assumes that you are running on a client computer running Windows and have already configured your command line interface with your account credentials and Region\. For more information, see [Configuring the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html)\.

In this example, include the following trust policy in the first command when you create the role\. This trust policy allows the Amazon EC2 service to assume the role\. 

```
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Principal": {"Service": "ec2.amazonaws.com"},
    "Action": "sts:AssumeRole"
  }
}
```

When you use the second command, you must attach a permissions policy to the role\. The following example permissions policy allows the role to perform only the `ListBucket` action on the `example_bucket` Amazon S3 bucket\.

```
{
  "Version": "2012-10-17",
  "Statement": {
    "Effect": "Allow",
    "Action": "s3:ListBucket",
    "Resource": "arn:aws:s3:::example_bucket"
  }
}
```

To create this `Test-Role-for-EC2` role, you must first save the previous trust policy with the name `trustpolicyforec2.json` and the previous permissions policy with the name `permissionspolicyforec2.json` to the `policies` directory in your local `C:` drive\. You can then use the following commands to create the role, attach the policy, create the instance profile, and add the role to the instance profile\.

```
# Create the role and attach the trust policy that allows EC2 to assume this role.
$ aws iam create-role --role-name Test-Role-for-EC2 --assume-role-policy-document file://C:\policies\trustpolicyforec2.json

# Embed the permissions policy (in this example an inline policy) to the role to specify what it is allowed to do.
$ aws iam put-role-policy --role-name Test-Role-for-EC2 --policy-name Permissions-Policy-For-Ec2 --policy-document file://C:\policies\permissionspolicyforec2.json

# Create the instance profile required by EC2 to contain the role
$ aws iam create-instance-profile --instance-profile-name EC2-ListBucket-S3

# Finally, add the role to the instance profile
$ aws iam add-role-to-instance-profile --instance-profile-name EC2-ListBucket-S3 --role-name Test-Role-for-EC2
```

When you launch the EC2 instance, specify the instance profile name in the **Configure Instance Details** page if you use the AWS console\. If you use the `aws ec2 run-instances` CLI command, specify the `--iam-instance-profile` parameter\.

## Creating a role for a service \(AWS API\)<a name="roles-creatingrole-service-api"></a>

### <a name="roles-creatingrole-servicerole-api"></a>

Creating a role from the AWS API involves multiple steps\. When you use the console to create a role, many of the steps are done for you, but with the API you must explicitly perform each step yourself\. You must create the role and then assign a permissions policy to the role\. If the service you are working with is Amazon EC2, then you must also create an instance profile and add the role to it\. Optionally, you can also set the [permissions boundary](access_policies_boundaries.md) for your role\.

**To create a role for an AWS service \(AWS API\)**

1. Create a role: [CreateRole](https://docs.aws.amazon.com/IAM/latest/APIReference/API_CreateRole.html)

   For the role's trust policy, you can specify a file location\.

1. Attach a managed permissions policy to the role: [AttachRolePolicy](https://docs.aws.amazon.com/IAM/latest/APIReference/API_AttachRolePolicy.html)

    or

   Create an inline permissions policy for the role: [PutRolePolicy](https://docs.aws.amazon.com/IAM/latest/APIReference/API_PutRolePolicy.html)

1. \(Optional\) Add custom attributes to the user by attaching tags: [TagRole](https://docs.aws.amazon.com/IAM/latest/APIReference/API_TagRole.html)

   For more information, see [Managing tags on IAM users \(AWS CLI or AWS API\)](id_tags_users.md#id_tags_users_procs-cli-api)\.

1. \(Optional\) Set the [permissions boundary](access_policies_boundaries.md) for the role: [PutRolePermissionsBoundary](https://docs.aws.amazon.com/IAM/latest/APIReference/API_PutRolePermissionsBoundary.html)

   A permissions boundary controls the maximum permissions that a role can have\. Permissions boundaries are an advanced AWS feature\.

If you are going to use the role with Amazon EC2 or another AWS service that uses Amazon EC2, you must store the role in an instance profile\. An instance profile is a container for a role\. Each instance profile can contain only one role, and that limit cannot be increased\. If you create the role in the AWS Management Console, the instance profile is created for you with the same name as the role\. For more information about instance profiles, see [Using instance profiles](id_roles_use_switch-role-ec2_instance-profiles.md)\. For information about how to launch an Amazon EC2 instance with a role, see [Controlling Access to Amazon EC2 Resources](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/UsingIAM.html#UsingIAMrolesWithAmazonEC2Instances) in the *Amazon EC2 User Guide for Linux Instances*\. 

**To create an instance profile and store the role in it \(AWS API\)**

1. Create an instance profile: [CreateInstanceProfile](https://docs.aws.amazon.com/IAM/latest/APIReference/API_CreateInstanceProfile.html)

1. Add the role to the instance profile: [AddRoleToInstanceProfile](https://docs.aws.amazon.com/IAM/latest/APIReference/API_AddRoleToInstanceProfile.html)