# Using service\-linked roles for AWS Identity and Access Management Access Analyzer<a name="access-analyzer-using-service-linked-roles"></a>

AWS Identity and Access Management Access Analyzer uses an IAM [ service\-linked role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_terms-and-concepts.html#iam-term-service-linked-role)\. A service\-linked role is a unique type of IAM role linked directly to Access Analyzer\. Service\-linked roles are predefined by Access Analyzer and include all the permissions that the feature requires to call other AWS services on your behalf\.

A service\-linked role makes setting up Access Analyzer easier because you don’t have to manually add the necessary permissions\. Access Analyzer defines the permissions of its service\-linked roles, and unless defined otherwise, only Access Analyzer can assume its roles\. The defined permissions include the trust policy and the permissions policy, and that permissions policy cannot be attached to any other IAM entity\.

For information about other services that support service\-linked roles, see [AWS Services That Work with IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_aws-services-that-work-with-iam.html) and look for the services that have **Yes** in the **Service\-Linked Role** column\. Choose a **Yes** with a link to view the service\-linked role documentation for that service\.

## Service\-linked role permissions for AWS Identity and Access Management Access Analyzer<a name="slr-permissions"></a>

AWS Identity and Access Management Access Analyzer uses the service\-linked role named **AWSServiceRoleForAccessAnalyzer** – Allow Access Analyzer to analyze resource metadata\.

The AWSServiceRoleForAccessAnalyzer service\-linked role trusts the following services to assume the role:
+ `access-analyzer.amazonaws.com`

The role permissions policy named [`AccessAnalyzerServiceRolePolicy`](security-iam-awsmanpol.md#security-iam-aa-service-role-policy) allows Access Analyzer to complete actions on specific resources\.

You must configure permissions to allow an IAM entity \(such as a user, group, or role\) to create, edit, or delete a service\-linked role\. For more information, see [Service\-Linked Role Permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#service-linked-role-permissions) in the *IAM User Guide*\.

## Creating a service\-linked role for Access Analyzer<a name="create-slr"></a>

You don't need to manually create a service\-linked role\. When you enable Access Analyzer in the AWS Management Console or the AWS API, Access Analyzer creates the service\-linked role for you\. The same service\-linked role is used in all Regions in which you enable IAM Access Analyzer\.

**Note**  
IAM Access Analyzer is Regional\. You must enable IAM Access Analyzer in each Region independently\.

If you delete this service\-linked role, IAM Access Analyzer recreates the role when you next create an analyzer\.

You can also use the IAM console to create a service\-linked role with the **Access Analyzer** use case\. In the AWS CLI or the AWS API, create a service\-linked role with the `access-analyzer.amazonaws.com` service name\. For more information, see [Creating a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#create-service-linked-role) in the *IAM User Guide*\. If you delete this service\-linked role, you can use this same process to create the role again\.

## Editing a service\-linked role for Access Analyzer<a name="edit-slr"></a>

Access Analyzer does not allow you to edit the AWSServiceRoleForAccessAnalyzer service\-linked role\. After you create a service\-linked role, you cannot change the name of the role because various entities might reference the role\. However, you can edit the description of the role using IAM\. For more information, see [Editing a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#edit-service-linked-role) in the *IAM User Guide*\.

## Deleting a service\-linked role for Access Analyzer<a name="delete-slr"></a>

If you no longer need to use a feature or service that requires a service\-linked role, we recommend that you delete that role\. That way you don’t have an unused entity that isn't actively monitored or maintained\. However, you must clean up the resources for your service\-linked role before you can manually delete it\.

**Note**  
If Access Analyzer is using the role when you try to delete the resources, then the deletion might fail\. If that happens, wait for a few minutes and try the operation again\.

**To delete Access Analyzer resources used by the AWSServiceRoleForAccessAnalyzer**

1. Open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the **Access reports** section, under **Access analyzer**, choose **Analyzers**\.

1. Choose the check box on the top left above the list of analyzers in the **Analyzers** table to select all analyzers\.

1. Choose **Delete**\.

1. To confirm that you want to delete the analyzers, enter **delete**, and then choose **Delete**\.

**To manually delete the service\-linked role using IAM**

Use the IAM console, the AWS CLI, or the AWS API to delete the AWSServiceRoleForAccessAnalyzer service\-linked role\. For more information, see [Deleting a Service\-Linked Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/using-service-linked-roles.html#delete-service-linked-role) in the *IAM User Guide*\.

## Supported Regions for Access Analyzer service\-linked roles<a name="slr-regions"></a>

Access Analyzer supports using service\-linked roles in all of the Regions where the service is available\. For more information, see [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html)\.