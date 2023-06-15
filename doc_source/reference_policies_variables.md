# IAM policy elements: Variables and tags<a name="reference_policies_variables"></a>

Use AWS Identity and Access Management \(IAM\) policy variables as placeholders when you don't know the exact value of a resource or condition key when you write the policy\.

**Note**  
If AWS cannot resolve a variable this might cause the entire statement to be invalid\. For example, if you use the `aws:TokenIssueTime` variable, the variable resolves to a value only when the requester authenticated using temporary credentials \(an IAM role\)\. To prevent variables from causing invalid statements, use the [\.\.\.IfExists condition operator\.](reference_policies_elements_condition_operators.md#Conditions_IfExists)

**Topics**
+ [Introduction](#policy-vars-intro)
+ [Using variables in policies](#policy-vars-using-variables)
+ [Tags as policy variables](#policy-vars-tags)
+ [Where you can use policy variables](#policy-vars-wheretouse)
+ [Policy variables with no value](#policy-vars-no-value)
+ [Request information that you can use for policy variables](#policy-vars-infotouse)
+ [Specifying default values](#policy-vars-default-values)
+ [For more information](#policy-vars-formoreinfo)

## Introduction<a name="policy-vars-intro"></a>

In IAM policies, many actions allow you to provide a name for the specific resources that you want to control access to\. For example, the following policy allows the user to list, read, and write objects with a prefix `David` in the Amazon S3 bucket `mybucket`\. 

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": ["s3:ListBucket"],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::mybucket"],
      "Condition": {"StringLike": {"s3:prefix": ["David/*"]}}
    },
    {
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::mybucket/David/*"]
    }
  ]
}
```

In some cases, you might not know the exact name of the resource when you write the policy\. You might want to generalize the policy so it works for many users without having to make a unique copy of the policy for each user\. For example, consider writing a policy to allow each user to have access to his or her own objects in an Amazon S3 bucket, as in the previous example\. Instead of creating a separate policy for each user that explicitly specifies the user's name as part of the resource, we recommend you create a single group policy that works for any user in that group\. 

## Using variables in policies<a name="policy-vars-using-variables"></a>

You can define dynamic values inside policies by using *policy variables* that set placeholders in a policy\. When the policy is evaluated, the policy variables are replaced with values that come from the conditional context keys passed in the request\. Global condition context keys can be used as variables in requests across AWS services\. Service specific condition keys can also be used as variables when interacting with AWS resources, but are only available when requests are made against resources which support them\. For a list of context keys available for each AWS service and resource, see the [https://docs.aws.amazon.com/service-authorization/latest/reference/reference.html](https://docs.aws.amazon.com/service-authorization/latest/reference/reference.html)\.

Variables can be used in [identity\-based policies, resource policies, service control policies, session policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html), and [VPC endpoint policies](https://docs.aws.amazon.com/vpc/latest/privatelink/vpc-endpoints-access.html)\. Identity\-based policies used as permissions boundaries also support policy variables\. 

Under certain circumstances, you can’t populate global condition context keys with a value\. To learn more about each key, see [https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html)\. 

**Important**  
Key names are case\-insensitive\. For example, `aws:CurrentTime` is equivalent to `AWS:currenttime`\.
You can use any single\-valued condition key as a variable\. You can't use a multivalued condition key as a variable\.

The following example shows a policy for an Amazon S3 bucket that uses a policy variable\. 

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": ["s3:ListBucket"],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::mybucket"],
      "Condition": {"StringLike": {"s3:prefix": ["${aws:username}/*"]}}
    },
    {
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::mybucket/${aws:username}/*"]
    }
  ]
}
```

When this policy is evaluated, IAM replaces the variable `${aws:username}`with the [friendly name](reference_identifiers.md#identifiers-friendly-names) of the actual current user\. This means that a single policy applied to a group of users can control access to a bucket\. It does this by using the user name as part of the resource's name\. 

The variable is marked using a `$` prefix followed by a pair of curly braces \(`{ }`\)\. Inside the `${ }` characters, you can include the name of the value from the request that you want to use in the policy\. The values you can use are discussed later on this page\.

**Note**  
In order to use policy variables, you must include the `Version` element in a statement, and the version must be set to a version that supports policy variables\. Variables were introduced in version `2012-10-17`\. Earlier versions of the policy language don't support policy variables\. If you don't include the `Version` element and set it to an appropriate version date, variables like `${aws:username}` are treated as literal strings in the policy\.   
A `Version` policy element is different from a policy version\. The `Version` policy element is used within a policy and defines the version of the policy language\. A policy version, on the other hand, is created when you change a customer managed policy in IAM\. The changed policy doesn't overwrite the existing policy\. Instead, IAM creates a new version of the managed policy\. To learn more about the `Version` policy element see [IAM JSON policy elements: Version](reference_policies_elements_version.md)\. To learn more about policy versions, see [Versioning IAM policies](access_policies_managed-versioning.md)\.

You can use policy variables in a similar way to allow each user to manage his or her own access keys\. A policy that allows a user to programmatically change the access key for user `David` looks like this: 

```
{
  "Version": "2012-10-17",
  "Statement": [{
    "Action": ["iam:*AccessKey*"],
    "Effect": "Allow",
    "Resource": ["arn:aws:iam::account-id:user/David"]
  }]
}
```

If this policy is attached to user `David`, that user can change his own access key\. As with the policies for accessing user\-specific Amazon S3 objects, you would have to create a separate policy for each user that includes the user's name\. You would then attach each policy to the individual users\. 

By using a policy variable, you can create a policy like this: 

```
{
  "Version": "2012-10-17",
  "Statement": [{
    "Action": ["iam:*AccessKey*"],
    "Effect": "Allow",
    "Resource": ["arn:aws:iam::account-id:user/${aws:username}"]
  }]
}
```

When you use a policy variable for the user name like this, you don't have to have a separate policy for each individual user\. Instead, you can attach this new policy to an IAM group that includes everyone who should be allowed to manage their own access keys\. When a user makes a request to modify his or her access key, IAM substitutes the user name from the current request for the `${aws:username}` variable and evaluates the policy\. 

## Tags as policy variables<a name="policy-vars-tags"></a>

In some AWS services you can attach your own custom attributes to resources that are created by those services\. For example, you can apply tags to Amazon S3 buckets or to IAM users\. These tags are key\-value pairs\. You define the tag key name and the value that is associated with that key name\. For example, you might create a tag with a **department** key and a **Human Resources** value\. For more information about tagging IAM entities, see [Tagging IAM resources](id_tags.md)\. For information about tagging resources created by other AWS services, see the documentation for that service\. For information about using Tag Editor, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html) in the *AWS Management Console User Guide*\.

You can tag IAM resources to simplify discovering, organizing, and tracking your IAM resources\. You can also tag IAM identities to control access to resources or to tagging itself\. To learn more about using tags to control access, see [Controlling access to and for IAM users and roles using tags](access_iam-tags.md)\. 

## Where you can use policy variables<a name="policy-vars-wheretouse"></a>

 You can use policy variables in the `Resource` element and in string comparisons in the `Condition` element\.

### Resource element<a name="policy-vars-resourceelement"></a>

You can use a policy variable in the `Resource` element, but only in the resource portion of the ARN\. This portion of the ARN appears after the fifth colon \(:\)\. You can't use a variable to replace parts of the ARN before the fifth colon, such as the service or account\. For more information about the ARN format, see [IAM ARNs](reference_identifiers.md#identifiers-arns)\.

The following policy might be attached to a group\. It gives each of the users in the group full programmatic access to a user\-specific object \(their own "home directory"\) in Amazon S3\. 

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Action": ["s3:ListBucket"],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::mybucket"],
      "Condition": {"StringLike": {"s3:prefix": ["${aws:username}/*"]}}
    },
    {
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Effect": "Allow",
      "Resource": ["arn:aws:s3:::mybucket/${aws:username}/*"]
    }
  ]
}
```

**Note**  
This example uses the `aws:username` key, which returns the user's friendly name \(like "Adele" or "David"\)\. Under some circumstances, you might want to use the `aws:userid` key instead, which is a globally unique value\. For more information, see [Unique identifiers](reference_identifiers.md#identifiers-unique-ids)\.

The following policy might be used for an IAM group\. It gives users in that group the ability to create, use, and delete queues that have their names and that are in the us\-east\-2 Region\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "ListForConsole",
            "Effect": "Allow",
            "Action": "sqs:ListQueues",
            "Resource": "*"
        },
        {
            "Sid": "AllQueueActions",
            "Effect": "Allow",
            "Action": "sqs:*",
            "Resource": "arn:aws:sqs:us-east-2:*:${aws:username}-queue"
        }
    ]
}
```

To replace part of an ARN with a tag value, surround the prefix and key name with $\{\}\. For example, the following `Resource` element refers to only a bucket that is named the same as the value in the requesting user's `department` tag\.

```
    "Resource": ["arn:aws:s3:::bucket/${aws:PrincipalTag/department}"]
```

### Condition element<a name="policy-vars-conditionelement"></a>

You can use a policy variable for `Condition` values in any condition that involves the string operators or the ARN operators\. String operators include `StringEquals`, `StringLike`, and `StringNotLike`\. ARN operators include `ArnEquals` and `ArnLike`\. You can't use a policy variable with other operators, such as `Numeric`, `Date`, `Boolean`, `Binary`, `IP Address`, or `Null` operators\. For more information about condition operators, see [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)\.

The following Amazon SNS topic policy gives users in AWS account `999999999999` the ability to manage \(perform all actions for\) the topic\. However this permission is granted only if the URL matches their AWS user name\. 

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Principal": {
        "AWS": "999999999999"
      },
      "Effect": "Allow",
      "Action": "sns:*",
      "Condition": {
        "StringLike": {
          "sns:endpoint": "https://example.com/${aws:username}/"
        },
        "StringEquals": {
          "sns:Protocol": "https"
        }
      }
    }
  ]
}
```

When referencing a tag in a `Condition` element expression, use the relevant prefix and key name as the condition key\. Then use the value that you want to test in the condition value\. For example, the following policy example allows full access to IAM users, but only if the tag `costCenter` is attached to the user\. The tag must also have a value of either `12345` or `67890`\. If the tag has no value, or has any other value, then the request fails\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
          "iam:*user*"
       ],
      "Resource": "*",
      "Condition": {
        "StringLike": {
          "iam:ResourceTag/costCenter": [ "12345", "67890" ]
        }
      }
    }
  ]
}
```

## Policy variables with no value<a name="policy-vars-no-value"></a>

When policy variables reference a condition context key that has no value or is not present in an authorization context for a request, the value is effectively null\. There is no equal or like value\. Condition context keys may not be present in the authorization context when:
+ You are using service specific condition context keys in requests to resources that do not support that condition key\.
+ Tags on IAM principals, sessions, resources, or requests are not present\.
+ Other circumstances as listed for each global condition context key in [AWS global condition context keys](reference_policies_condition-keys.md)\.

When you use a variable with no value in the condition element of an IAM policy, [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md) like `StringEquals` or `StringLike` do not match, and the policy statement does not take effect\.

Inverted condition operators like `StringNotEquals` or `StringNotLike` do match against a null value, as the value of the condition key they are testing against is not equal to or like the effectively null value\.

For example, `aws:principaltag/Team` must be equal to `s3:ExistingObjectTag/Team` to allow access\. Access is specifically denied when `aws:principaltag/Team` is not set\. If a variable that has no value in the authorization context is used as part of the `Resource` or `NotResource` element of a policy, the resource that includes a policy variable with no value will not match any resource\.

```
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::/example-bucket/*",
        "StringNotEquals": {
          "s3:ExistingObjectTag/Team": "${aws:PrincipalTag/Team}"
        }
      }
    }
  ]
}
```

## Request information that you can use for policy variables<a name="policy-vars-infotouse"></a>

 You can use the `Condition` element of a JSON policy to compare keys in the [request context](reference_policies_evaluation-logic.md#policy-eval-reqcontext) with key values that you specify in your policy\. When you use a policy variable, AWS substitutes a value from the request context key in place of the variable in your policy\.

### Principal key values<a name="principaltable"></a>

The values for `aws:username`, `aws:userid`, and `aws:PrincipalType` depend on what type of principal initiated the request\. For example, the request could be made using the credentials of an IAM user, an IAM role, or the AWS account root user\. The following shows values for these keys for different types of principals\. 

For the items in this note the following:
+ *not present* means that the value is not in the current request information, and any attempt to match it fails and causes the statement to be invalid\. 
+ *role\-id* is a unique identifier assigned to each role at creation\. You can display the role ID with the AWS CLI command: `aws iam get-role --role-name rolename`
+ *caller\-specified\-name* and *caller\-specified\-role\-name* are names that are passed by the calling process \(such as an application or service\) when it makes a call to get temporary credentials\.
+ *ec2\-instance\-id* is a value assigned to the instance when it is launched and appears on the **Instances** page of the Amazon EC2 console\. You can also display the instance ID by running the AWS CLI command: `aws ec2 describe-instances`

### Information available in requests for federated users<a name="policy-vars-infoWIF"></a>

Federated users are users who are authenticated using a system other than IAM\. For example, a company might have an application for use in\-house that makes calls to AWS\. It might be impractical to give an IAM identity to every corporate user who uses the application\. Instead, the company might use a proxy \(middle\-tier\) application that has a single IAM identity, or the company might use a SAML identity provider \(IdP\)\. The proxy application or SAML IdP authenticates individual users using the corporate network\. A proxy application can then use its IAM identity to get temporary security credentials for individual users\. A SAML IdP can in effect exchange identity information for AWS temporary security credentials\. The temporary credentials can then be used to access AWS resources\. 

Similarly, you might create an app for a mobile device in which the app needs to access AWS resources\. In that case, you might use *web identity federation*, where the app authenticates the user using a well\-known identity provider like Login with Amazon, Amazon Cognito, Facebook, or Google\. The app can then use the user's authentication information from these providers to get temporary security credentials for accessing AWS resources\. 

The recommended way to use web identity federation is by taking advantage of Amazon Cognito and the AWS mobile SDKs\. For more information, see the following:
+ [Amazon Cognito User Guide](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-identity.html)\. 
+ [Common scenarios for temporary credentials](id_credentials_temp.md#sts-introduction)\.

### Special characters<a name="policy-vars-specialchars"></a>

There are a few special predefined policy variables that have fixed values that enable you to represent characters that otherwise have special meaning\. If these special characters are part of the string, you are trying to match and you inserted them literally they would be misinterpreted\. For example, inserting an \* asterisk in the string would be interpreted as a wildcard, matching any characters, instead of as a literal \*\. In these cases, you can use the following predefined policy variables:
+ **$\{\*\}** \- use where you need an \* \(asterisk\) character\.
+ **$\{?\}** \- use where you need a ? \(question mark\) character\.
+ **$\{$\}** \- use where you need a $ \(dollar sign\) character\.

These predefined policy variables can be used in any string where you can use regular policy variables\.

## Specifying default values<a name="policy-vars-default-values"></a>

To add a default value to a variable, surround the default value with single quotes \(`' '`\), and separate the variable text and the default value with a comma and space \(`, `\)\.

For example, if a principal is tagged with `team=yellow`, they can access `ExampleCorp's` Amazon S3 bucket named `DOC-EXAMPLE-BUCKET-yellow`\. A policy with this resource allows team members to access their team bucket, but not those of other teams\. For users without team tags, it sets a default value of `company-wide` for the bucket name\. These users can access only the `DOC-EXAMPLE-BUCKET-company-wide` bucket where they can view broad information, such as instructions for joining a team\.

```
"Resource":"arn:aws:s3:::DOC-EXAMPLE-BUCKET-${aws:PrincipalTag/team, 'company-wide'}"
```

## For more information<a name="policy-vars-formoreinfo"></a>

For more information about policies, see the following: 
+  [Policies and permissions in IAM](access_policies.md) 
+  [Example IAM identity\-based policies](access_policies_examples.md) 
+  [IAM JSON policy elements reference](reference_policies_elements.md) 
+  [Policy evaluation logic](reference_policies_evaluation-logic.md) 
+  [About web identity federation](id_roles_providers_oidc.md)