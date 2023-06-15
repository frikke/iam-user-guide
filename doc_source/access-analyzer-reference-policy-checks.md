# Access Analyzer policy check reference<a name="access-analyzer-reference-policy-checks"></a>

You can validate your policies using AWS IAM Access Analyzer policy checks\. You can create or edit a policy using the AWS CLI, AWS API, or JSON policy editor in the IAM console\. Access Analyzer validates your policy against IAM [policy grammar](reference_policies_grammar.md) and [best practices](best-practices.md)\. You can view policy validation check findings that include security warnings, errors, general warnings, and suggestions for your policy\. These findings provide actionable recommendations that help you author policies that are functional and conform to security best practices\. To learn more about validating policies using Access Analyzer, see [IAM Access Analyzer policy validation](access-analyzer-policy-validation.md)\.

## Error – ARN account not allowed<a name="access-analyzer-reference-policy-checks-error-arn-account-not-allowed"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
ARN account not allowed: The service {{service}} does not support specifying an account ID in the resource ARN.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The service {{service}} does not support specifying an account ID in the resource ARN."
```

**Resolving the error**

Remove the account ID from the resource ARN\. The resource ARNs for some AWS services do not support specifying an account ID\.

For example, Amazon S3 does not support an account ID as a namespace in bucket ARNs\. An Amazon S3 bucket name is globally unique, and the namespace is shared by all AWS accounts\. To view all of the resource types available in Amazon S3, see [ Resource types defined by Amazon S3](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazons3.html#amazons3-resources-for-iam-policies) in the *Service Authorization Reference*\.

**Related terms**
+ [Policy resources](reference_policies_elements_resource.md)
+ [Account Identifiers](https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html)
+ [Resource ARNs](reference_identifiers.md#identifiers-arns)
+ [AWS service resources with ARN formats](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – ARN Region not allowed<a name="access-analyzer-reference-policy-checks-error-arn-region-not-allowed"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
ARN Region not allowed: The service {{service}} does not support specifying a Region in the resource ARN.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The service {{service}} does not support specifying a Region in the resource ARN."
```

**Resolving the error**

Remove the Region from the resource ARN\. The resource ARNs for some AWS services do not support specifying a Region\.

For example, IAM is a global service\. The Region portion of an IAM resource ARN is always kept blank\. IAM resources are global, like an AWS account is today\. For example, after you sign in as an IAM user, you can access AWS services in any geographic region\.
+ [Policy resources](reference_policies_elements_resource.md)
+ [Resource ARNs](reference_identifiers.md#identifiers-arns)
+ [AWS service resources with ARN formats](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Data type mismatch<a name="access-analyzer-reference-policy-checks-error-data-type-mismatch"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Data type mismatch: The text does not match the expected JSON data type {{data_type}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The text does not match the expected JSON data type {{data_type}}."
```

**Resolving the error**

Update the text to use the supported data type\.

For example, the `Version` global condition key requires a `String` data type\. If you provide a date or an integer, the data type won't match\.

**Related terms**
+ [Global condition keys](reference_policies_condition-keys.md)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)

## Error – Duplicate keys with different case<a name="access-analyzer-reference-policy-checks-error-duplicate-keys-with-different-case"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Duplicate keys with different case: The condition key {{key}} appears more than once with different capitalization in the same condition block. Remove the duplicate condition keys.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition key {{key}} appears more than once with different capitalization in the same condition block. Remove the duplicate condition keys."
```

**Resolving the error**

Review the similar condition keys within the same condition block and use the same capitalization for all instances\.

A *condition block* is the text within the `Condition` element of a policy statement\. Condition key *names* are not case\-sensitive\. The case\-sensitivity of condition key *values* depends on the condition operator that you use\. For more information about case\-sensitivity in condition keys, see [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)\.

**Related terms**
+ [Conditions](reference_policies_elements_condition.md)
+ [Condition block](reference_policies_elements_condition.md#AccessPolicyLanguage_ConditionBlock)
+ [Global condition keys](reference_policies_condition-keys.md)
+ [AWS service condition keys](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid action<a name="access-analyzer-reference-policy-checks-error-invalid-action"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid action: The action {{action}} does not exist. Did you mean {{valid_action}}?
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The action {{action}} does not exist. Did you mean {{valid_action}}?"
```

**Resolving the error**

The action that you specified is not valid\. This can happen if you mis\-type the service prefix or the action name\. For some common issues, the policy check returns a suggested action\.

**Related terms**
+ [Policy actions](reference_policies_elements_action.md)
+ [AWS service actions](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

### AWS managed policies with this error<a name="accan-ref-policy-check-message-fix-error-invalid-action-awsmanpol"></a>

[AWS managed policies](access_policies_managed-vs-inline.md#aws-managed-policies) enable you to get started with AWS by assigning permissions based on general AWS use cases\.

The following AWS managed policies include invalid actions in their policy statements\. Invalid actions do not affect the permissions granted by the policy\. When using an AWS managed policy as a reference to create your managed policy, AWS recommends that you remove invalid actions from your policy\.
+ [AmazonEMRFullAccessPolicy\_v2](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AmazonEMRFullAccessPolicy_v2)
+ [CloudWatchSyntheticsFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/CloudWatchSyntheticsFullAccess)

## Error – Invalid ARN account<a name="access-analyzer-reference-policy-checks-error-invalid-arn-account"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid ARN account: The resource ARN account ID {{account}} is not valid. Provide a 12-digit account ID.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The resource ARN account ID {{account}} is not valid. Provide a 12-digit account ID."
```

**Resolving the error**

Update the account ID in the resource ARN\. Account IDs are 12\-digit integers\. To learn how to view your account ID, see [Finding your AWS account ID](https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html#FindingYourAccountIdentifiers)\.

**Related terms**
+ [Policy resources](reference_policies_elements_resource.md)
+ [Account Identifiers](https://docs.aws.amazon.com/general/latest/gr/acct-identifiers.html)
+ [Resource ARNs](reference_identifiers.md#identifiers-arns)
+ [AWS service resources with ARN formats](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid ARN prefix<a name="access-analyzer-reference-policy-checks-error-invalid-arn-prefix"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid ARN prefix: Add the required prefix (arn) to the resource ARN.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add the required prefix (arn) to the resource ARN."
```

**Resolving the error**

AWS resource ARNs must include the required `arn:` prefix\.

**Related terms**
+ [Policy resources](reference_policies_elements_resource.md)
+ [Resource ARNs](reference_identifiers.md#identifiers-arns)
+ [AWS service resources with ARN formats](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid ARN Region<a name="access-analyzer-reference-policy-checks-error-invalid-arn-region"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid ARN Region: The Region {{region}} is not valid for this resource. Update the resource ARN to include a supported Region.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The Region {{region}} is not valid for this resource. Update the resource ARN to include a supported Region."
```

**Resolving the error**

The resource type is not supported in the specified Region\. For a table of AWS services supported in each Region, see the [Region table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)\.

**Related terms**
+ [Policy resources](reference_policies_elements_resource.md)
+ [Resource ARNs](reference_identifiers.md#identifiers-arns)
+ [Region names and codes](https://docs.aws.amazon.com/general/latest/gr/rande.html#region-names-codes)

## Error – Invalid ARN resource<a name="access-analyzer-reference-policy-checks-error-invalid-arn-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid ARN resource: Resource ARN does not match the expected ARN format. Update the resource portion of the ARN.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Resource ARN does not match the expected ARN format. Update the resource portion of the ARN."
```

**Resolving the error**

The resource ARN must match the specifications for known resource types\. To view the expected ARN format for a service, see [Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)\. Choose the name of the service to view its resource types and ARN formats\.

**Related terms**
+ [Policy resources](reference_policies_elements_resource.md)
+ [Resource ARNs](reference_identifiers.md#identifiers-arns)
+ [AWS service resources with ARN formats](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid ARN service case<a name="access-analyzer-reference-policy-checks-error-invalid-arn-service-case"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid ARN service case: Update the service name ${service} in the resource ARN to use all lowercase letters.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Update the service name ${service} in the resource ARN to use all lowercase letters."
```

**Resolving the error**

The service in the resource ARN must match the specifications \(including capitalization\) for service prefixes\. To view the prefix for a service, see [Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)\. Choose the name of the service and locate its prefix in the first sentence\.

**Related terms**
+ [Policy resources](reference_policies_elements_resource.md)
+ [Resource ARNs](reference_identifiers.md#identifiers-arns)
+ [AWS service resources with ARN formats](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid condition data type<a name="access-analyzer-reference-policy-checks-error-invalid-condition-data-type"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid condition data type: The condition value data types do not match. Use condition values of the same JSON data type.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition value data types do not match. Use condition values of the same JSON data type."
```

**Resolving the error**

The value in the condition key\-value pair must match the data type of the condition key and condition operator\. To view the condition key data type for a service, see [Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)\. Choose the name of the service to view the condition keys for that service\.

For example, the [`CurrentTime`](reference_policies_condition-keys.md#condition-keys-currenttime) global condition key supports the `Date` condition operator\. If you provide a string or an integer for the value in the condition block, the data type won't match\.

**Related terms**
+ [Conditions](reference_policies_elements_condition.md)
+ [Condition block](reference_policies_elements_condition.md#AccessPolicyLanguage_ConditionBlock)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)
+ [Global condition keys](reference_policies_condition-keys.md)
+ [AWS service condition keys](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid condition key format<a name="access-analyzer-reference-policy-checks-error-invalid-condition-key-format"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid condition key format: The condition key format is not valid. Use the format service:keyname.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition key format is not valid. Use the format service:keyname."
```

**Resolving the error**

The key in the condition key\-value pair must match the specifications for the service\. To view the condition keys for a service, see [Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)\. Choose the name of the service to view the condition keys for that service\.

**Related terms**
+ [Conditions](reference_policies_elements_condition.md)
+ [Global condition keys](reference_policies_condition-keys.md)
+ [AWS service condition keys](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid condition multiple Boolean<a name="access-analyzer-reference-policy-checks-error-invalid-condition-multiple-boolean"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid condition multiple Boolean: The condition key does not support multiple Boolean values. Use a single Boolean value.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition key does not support multiple Boolean values. Use a single Boolean value."
```

**Resolving the error**

The key in the condition key\-value pair expects a single Boolean value\. When you provide multiple Boolean values, the condition match might not return the results that you expect\.

To view the condition keys for a service, see [Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)\. Choose the name of the service to view the condition keys for that service\.
+ [Conditions](reference_policies_elements_condition.md)
+ [Global condition keys](reference_policies_condition-keys.md)
+ [AWS service condition keys](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid condition operator<a name="access-analyzer-reference-policy-checks-error-invalid-condition-operator"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid condition operator: The condition operator {{operator}} is not valid. Use a valid condition operator.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition operator {{operator}} is not valid. Use a valid condition operator."
```

**Resolving the error**

Update the condition to use a supported condition operator\.

**Related terms**
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)
+ [Condition element](reference_policies_elements_condition.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Error – Invalid effect<a name="access-analyzer-reference-policy-checks-error-invalid-effect"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid effect: The effect {{effect}} is not valid. Use Allow or Deny.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The effect {{effect}} is not valid. Use Allow or Deny."
```

**Resolving the error**

Update the `Effect` element to use a valid effect\. Valid values for `Effect` are **Allow** and **Deny**\.

**Related terms**
+ [Effect element](reference_policies_elements_effect.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Error – Invalid global condition key<a name="access-analyzer-reference-policy-checks-error-invalid-global-condition-key"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid global condition key: The condition key {{key}} does not exist. Use a valid condition key.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition key {{key}} does not exist. Use a valid condition key."
```

**Resolving the error**

Update the condition key in the condition key\-value pair to use a supported global condition key\.

Global condition keys are condition keys with an `aws:` prefix\. AWS services can support global condition keys or provide service\-specific keys that include their service prefix\. For example, IAM condition keys include the `iam:` prefix\. For more information, see  [Actions, Resources, and Condition Keys for AWS Services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)  and choose the service whose keys you want to view\.

**Related terms**
+ [Global condition keys](reference_policies_condition-keys.md)

## Error – Invalid partition<a name="access-analyzer-reference-policy-checks-error-invalid-partition"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid partition: The resource ARN for the service {{service}} does not support the partition {{partition}}. Use the supported values: {{partitions}}
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The resource ARN for the service {{service}} does not support the partition {{partition}}. Use the supported values: {{partitions}}"
```

**Resolving the error**

Update the resource ARN to include a supported partition\. If you included a supported partition, then the service or resource might not support the partition that you included\.

A *partition* is a group of AWS Regions\. Each AWS account is scoped to one partition\. In Classic Regions, use the `aws` partition\. In China Regions, use `aws-cn`\.

**Related terms**
+ [Amazon Resource Names \(ARNs\) \- Partitions](https://docs.aws.amazon.com/general/latest/gr/aws-arns-and-namespaces.html)

## Error – Invalid policy element<a name="access-analyzer-reference-policy-checks-error-invalid-policy-element"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid policy element: The policy element {{element}} is not valid.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The policy element {{element}} is not valid."
```

**Resolving the error**

Update the policy to include only supported JSON policy elements\.

**Related terms**
+ [JSON policy elements](reference_policies_elements.md)

## Error – Invalid principal format<a name="access-analyzer-reference-policy-checks-error-invalid-principal-format"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid principal format: The Principal element contents are not valid. Specify a key-value pair in the Principal element.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The Principal element contents are not valid. Specify a key-value pair in the Principal element."
```

**Resolving the error**

Update the principal to use a supported key\-value pair format\. 

You can specify a principal in a resource\-based policy, but not an identity\-based policy\. 

For example, to define access for everyone in an AWS account, use the following principal in your policy:

```
"Principal": { "AWS": "123456789012" }
```

**Related terms**
+ [JSON policy elements: Principal](reference_policies_elements_principal.md)
+ [Identity\-based policies and resource\-based policies](access_policies_identity-vs-resource.md)

## Error – Invalid principal key<a name="access-analyzer-reference-policy-checks-error-invalid-principal-key"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid principal key: The principal key {{principal-key}} is not valid.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The principal key {{principal-key}} is not valid."
```

**Resolving the error**

Update the key in the principal key\-value pair to use a supported principal key\. The following are supported principal keys:
+ AWS
+ CanonicalUser
+ Federated
+ Service

**Related terms**
+ [Principal element](reference_policies_elements_principal.md)

## Error – Invalid Region<a name="access-analyzer-reference-policy-checks-error-invalid-region"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid Region: The Region {{region}} is not valid. Update the condition value to a suported Region.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The Region {{region}} is not valid. Update the condition value to a suported Region."
```

**Resolving the error**

Update the value of the condition key\-value pair to include a supported Region\. For a table of AWS services supported in each Region, see the [Region table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)\.

**Related terms**
+ [Policy resources](reference_policies_elements_resource.md)
+ [Resource ARNs](reference_identifiers.md#identifiers-arns)
+ [Region names and codes](https://docs.aws.amazon.com/general/latest/gr/rande.html#region-names-codes)

## Error – Invalid service<a name="access-analyzer-reference-policy-checks-error-invalid-service"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid service: The service {{service}} does not exist. Use a valid service name.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The service {{service}} does not exist. Use a valid service name."
```

**Resolving the error**

The service prefix in the action or condition key must match the specifications \(including capitalization\) for service prefixes\. To view the prefix for a service, see [ Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)\. Choose the name of the service and locate its prefix in the first sentence\.

**Related terms**
+ [ Known services and their actions, resources, and condition keys](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid service condition key<a name="access-analyzer-reference-policy-checks-error-invalid-service-condition-key"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid service condition key: The condition key {{key}} does not exist in the service {{service}}. Use a valid condition key.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition key {{key}} does not exist in the service {{service}}. Use a valid condition key."
```

**Resolving the error**

Update the key in the condition key\-value pair to use a known condition key for the service\. Global condition key names begin with the `aws` prefix\. AWS services can provide service\-specific keys that include their service prefix\. To view the prefix for a service, see [ Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)\.

**Related terms**
+ [Global condition keys](reference_policies_condition-keys.md)
+ [ Known services and their actions, resources, and condition keys](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid service in action<a name="access-analyzer-reference-policy-checks-error-invalid-service-in-action"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid service in action: The service {{service}} specified in the action does not exist. Did you mean {{service2}}?
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The service {{service}} specified in the action does not exist. Did you mean {{service2}}?"
```

**Resolving the error**

The service prefix in the action must match the specifications \(including capitalization\) for service prefixes\. To view the prefix for a service, see [ Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)\. Choose the name of the service and locate its prefix in the first sentence\.

**Related terms**
+ [Action element](reference_policies_elements_action.md)
+ [ Known services and their actions](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid variable for operator<a name="access-analyzer-reference-policy-checks-error-invalid-variable-for-operator"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid variable for operator: Policy variables can only be used with String and ARN operators.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Policy variables can only be used with String and ARN operators."
```

**Resolving the error**

You can use policy variables in the `Resource` element and in string comparisons in the `Condition` element\. Conditions support variables when you use string operators or ARN operators\. String operators include `StringEquals`, `StringLike`, and `StringNotLike`\. ARN operators include `ArnEquals` and `ArnLike`\. You can't use a policy variable with other operators, such as Numeric, Date, Boolean,  Binary, IP Address, or Null operators\.

**Related terms**
+ [Using policy variables in the Condition element](reference_policies_variables.md#policy-vars-conditionelement)
+ [Condition element](reference_policies_elements_condition.md)

## Error – Invalid version<a name="access-analyzer-reference-policy-checks-error-invalid-version"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid version: The version ${version} is not valid. Use one of the following versions: ${versions}
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The version ${version} is not valid. Use one of the following versions: ${versions}"
```

**Resolving the error**

The `Version` policy element specifies the language syntax rules that AWS uses to process a policy\. To use all of the available policy features, include the latest `Version` element before the `Statement` element in all of your policies\.

```
"Version": "2012-10-17"
```

**Related terms**
+ [Version element](reference_policies_elements_version.md)

## Error – Json syntax error<a name="access-analyzer-reference-policy-checks-error-json-syntax-error"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Json syntax error: Fix the JSON syntax error at index {{index}} line {{line}} column {{column}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Fix the JSON syntax error at index {{index}} line {{line}} column {{column}}."
```

**Resolving the error**

Your policy includes a syntax error\. Check your JSON syntax\.

**Related terms**
+ [JSON validator](https://jsonlint.com/)
+ [IAM JSON policy elements reference](reference_policies_elements.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Error – Json syntax error<a name="access-analyzer-reference-policy-checks-error-json-syntax-error"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Json syntax error: Fix the JSON syntax error.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Fix the JSON syntax error."
```

**Resolving the error**

Your policy includes a syntax error\. Check your JSON syntax\.

**Related terms**
+ [JSON validator](https://jsonlint.com/)
+ [IAM JSON policy elements reference](reference_policies_elements.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Error – Missing action<a name="access-analyzer-reference-policy-checks-error-missing-action"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing action: Add an Action or NotAction element to the policy statement.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add an Action or NotAction element to the policy statement."
```

**Resolving the error**

AWS JSON policies must include an `Action` or `NotAction` element\.

**Related terms**
+ [Action element](reference_policies_elements_action.md)
+ [NotAction element](reference_policies_elements_notaction.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Error – Missing ARN field<a name="access-analyzer-reference-policy-checks-error-missing-arn-field"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing ARN field: Resource ARNs must include at least {{fields}} fields in the following structure: arn:partition:service:region:account:resource
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Resource ARNs must include at least {{fields}} fields in the following structure: arn:partition:service:region:account:resource"
```

**Resolving the error**

All of the fields in the resource ARN must match the specifications for a known resource type\. To view the expected ARN format for a service, see [Actions, resources, and condition keys for AWS services](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)\. Choose the name of the service to view its resource types and ARN formats\.

**Related terms**
+ [Policy resources](reference_policies_elements_resource.md)
+ [Resource ARNs](reference_identifiers.md#identifiers-arns)
+ [AWS service resources with ARN formats](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Missing ARN Region<a name="access-analyzer-reference-policy-checks-error-missing-arn-region"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing ARN Region: Add a Region to the {{service}} resource ARN.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add a Region to the {{service}} resource ARN."
```

**Resolving the error**

The resource ARNs for most AWS services require that you specify a Region\. For a table of AWS services supported in each Region, see the [Region table](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)\.

**Related terms**
+ [Policy resources](reference_policies_elements_resource.md)
+ [Resource ARNs](reference_identifiers.md#identifiers-arns)
+ [Region names and codes](https://docs.aws.amazon.com/general/latest/gr/rande.html#region-names-codes)

## Error – Missing effect<a name="access-analyzer-reference-policy-checks-error-missing-effect"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing effect: Add an Effect element to the policy statement with a value of Allow or Deny.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add an Effect element to the policy statement with a value of Allow or Deny."
```

**Resolving the error**

AWS JSON policies must include an `Effect` element with a value of **Allow** and **Deny**\.

**Related terms**
+ [Effect element](reference_policies_elements_effect.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Error – Missing principal<a name="access-analyzer-reference-policy-checks-error-missing-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing principal: Add a Principal element to the policy statement.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add a Principal element to the policy statement."
```

**Resolving the error**

Resource\-based policies must include a `Principal` element\.

For example, to define access for everyone in an AWS account, use the following principal in your policy:

```
"Principal": { "AWS": "123456789012" }
```

**Related terms**
+ [Principal element](reference_policies_elements_principal.md)
+ [Identity\-based policies and resource\-based policies](access_policies_identity-vs-resource.md)

## Error – Missing qualifier<a name="access-analyzer-reference-policy-checks-error-missing-qualifier"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing qualifier: The request context key ${key} has multiple values. Use the ForAllValues or ForAnyValue condition key qualifiers in your policy.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The request context key ${key} has multiple values. Use the ForAllValues or ForAnyValue condition key qualifiers in your policy."
```

**Resolving the error**

In the `Condition` element, you build expressions in which you use condition operators like equal or less than to compare a condition in the policy against keys and values in the request context\. For requests that include multiple values for a single condition key, you must enclose the conditions within brackets like an array \("Key2":\["Value2A", "Value2B"\]\)\. You must also use the `ForAllValues` or `ForAnyValue`  set operators with the `StringLike` condition operator\. These qualifiers add set\-operation functionality to the condition operator so that you can test multiple request values against multiple condition values\.

**Related terms**
+ [Using multiple condition keys and values](reference_policies_multi-value-conditions.md#reference_policies_multi-key-or-value-conditions)
+ [Condition element](reference_policies_elements_condition.md)

### AWS managed policies with this error<a name="accan-ref-policy-check-message-fix-error-missing-qualifier-awsmanpol"></a>

[AWS managed policies](access_policies_managed-vs-inline.md#aws-managed-policies) enable you to get started with AWS by assigning permissions based on general AWS use cases\.

The following AWS managed policies include a missing qualifier for condition keys in their policy statements\. When using the AWS managed policy as a reference to create your customer managed policy, AWS recommends that you add the `ForAllValues` or `ForAnyValue` condition key qualifiers to your `Condition` element\.
+ [AWSGlueConsoleSageMakerNotebookFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AWSGlueConsoleSageMakerNotebookFullAccess)

## Error – Missing resource<a name="access-analyzer-reference-policy-checks-error-missing-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing resource: Add a Resource or NotResource element to the policy statement.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add a Resource or NotResource element to the policy statement."
```

**Resolving the error**

Identity\-based policies must include a `Resource` or `NotResource` element\.

**Related terms**
+ [Resource element](reference_policies_elements_resource.md)
+ [NotResource element](reference_policies_elements_notresource.md)
+ [Identity\-based policies and resource\-based policies](access_policies_identity-vs-resource.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Error – Missing statement<a name="access-analyzer-reference-policy-checks-error-missing-statement"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing statement: Add a statement to the policy
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add a statement to the policy"
```

**Resolving the error**

A JSON policy must include a statement\.

**Related terms**
+ [JSON policy elements](reference_policies_elements.md)

## Error – Null with if exists<a name="access-analyzer-reference-policy-checks-error-null-with-if-exists"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Null with if exists: The Null condition operator cannot be used with the IfExists suffix. Update the operator or the suffix.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The Null condition operator cannot be used with the IfExists suffix. Update the operator or the suffix."
```

**Resolving the error**

You can add `IfExists` to the end of any condition operator name except the `Null` condition operator\. Use a `Null` condition operator to check if a condition key is present at the time of authorization\. Use `...ifExists` to say "If the policy key is present in the context of the request, process the key as specified in the policy\. If the key is not present, evaluate the condition element as true\."

**Related terms**
+ [\.\.\.IfExists condition operators](reference_policies_elements_condition_operators.md#Conditions_IfExists)
+ [Null condition operator](reference_policies_elements_condition_operators.md#Conditions_Null)
+ [Condition element](reference_policies_elements_condition.md)

## Error – SCP syntax error action wildcard<a name="access-analyzer-reference-policy-checks-error-scp-syntax-error-action-wildcard"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
SCP syntax error action wildcard: SCP actions can include wildcards (*) only at the end of a string. Update {{action}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "SCP actions can include wildcards (*) only at the end of a string. Update {{action}}."
```

**Resolving the error**

AWS Organizations service control policies \(SCPs\) support specifying values in the `Action` or `NotAction` elements\. However, these values can include wildcards \(\*\) only at the end of the string\. This means that you can specify `iam:Get*` but not `iam:*role`\.

To specify multiple actions, AWS recommends that you list them individually\.

**Related terms**
+ [SCP Action and NotAction elements](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_syntax.html#scp-syntax-action)
+ [Strategies for using SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_strategies.html)
+ [AWS Organizations service control policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
+ [IAM JSON policy elements: Action](reference_policies_elements_action.md)

## Error – SCP syntax error allow condition<a name="access-analyzer-reference-policy-checks-error-scp-syntax-error-allow-condition"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
SCP syntax error allow condition: SCPs do not support the Condition element with effect Allow. Update the element Condition or the effect.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "SCPs do not support the Condition element with effect Allow. Update the element Condition or the effect."
```

**Resolving the error**

AWS Organizations service control policies \(SCPs\) support specifying values in the `Condition` element only when you use `"Effect": "Deny"`\.

To allow only a single action, you can deny access to everything except the condition that you specify using the `...NotEquals` version of a condition operator\. This negates the comparison made by the operator\.

**Related terms**
+ [SCP Condition element](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_syntax.html#scp-syntax-condition)
+ [Strategies for using SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_strategies.html)
+ [AWS Organizations service control policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
+ [Example policy: Denies access to AWS based on the requested Region](reference_policies_examples_aws_deny-requested-region.md)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Error – SCP syntax error allow NotAction<a name="access-analyzer-reference-policy-checks-error-scp-syntax-error-allow-notaction"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
SCP syntax error allow NotAction: SCPs do not support NotAction with effect Allow. Update the element NotAction or the effect.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "SCPs do not support NotAction with effect Allow. Update the element NotAction or the effect."
```

**Resolving the error**

AWS Organizations service control policies \(SCPs\) do not support using the `NotAction` element with `"Effect": "Allow"`\.

You must rewrite the logic to allow a list of actions, or to deny every action that is not listed\.

**Related terms**
+ [SCP Action and NotAction elements](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_syntax.html#scp-syntax-action)
+ [Strategies for using SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_strategies.html)
+ [AWS Organizations service control policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
+ [IAM JSON policy elements: Action](reference_policies_elements_action.md)

## Error – SCP syntax error allow resource<a name="access-analyzer-reference-policy-checks-error-scp-syntax-error-allow-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
SCP syntax error allow resource: SCPs do not support Resource with effect Allow. Update the element Resource or the effect.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "SCPs do not support Resource with effect Allow. Update the element Resource or the effect."
```

**Resolving the error**

AWS Organizations service control policies \(SCPs\) support specifying values in the `Resource` element only when you use `"Effect": "Deny"`\.

You must rewrite the logic to allow all resources, or to deny every resource that is listed\.

**Related terms**
+ [SCP Resource element](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_syntax.html#scp-syntax-resource)
+ [Strategies for using SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_strategies.html)
+ [AWS Organizations service control policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## Error – SCP syntax error NotResource<a name="access-analyzer-reference-policy-checks-error-scp-syntax-error-notresource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
SCP syntax error NotResource: SCPs do not support the NotResource element. Update the policy to use Resource instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "SCPs do not support the NotResource element. Update the policy to use Resource instead."
```

**Resolving the error**

AWS Organizations service control policies \(SCPs\) do not support the `NotResource` element\.

You must rewrite the logic to allow all resources, or to deny every resource that is listed\.

**Related terms**
+ [SCP Resource element](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_syntax.html#scp-syntax-resource)
+ [Strategies for using SCPs](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_strategies.html)
+ [AWS Organizations service control policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## Error – SCP syntax error principal<a name="access-analyzer-reference-policy-checks-error-scp-syntax-error-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
SCP syntax error principal: SCPs do not support specifying principals. Remove the Principal or NotPrincipal element.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "SCPs do not support specifying principals. Remove the Principal or NotPrincipal element."
```

**Resolving the error**

AWS Organizations service control policies \(SCPs\) do not support the `Principal` or `NotPrincipal` elements\.

You can specify the Amazon Resource Name \(ARN\) using the `aws:PrincipalArn` global condition key in the `Condition` element\.

**Related terms**
+ [SCP syntax](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_syntax.html)
+ [Global condition keys for principals](reference_policies_condition-keys.md#condition-keys-principalarn)

## Error – Unique Sids required<a name="access-analyzer-reference-policy-checks-error-unique-sids-required"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unique Sids required: Duplicate statement IDs are not supported for this policy type. Update the Sid value.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Duplicate statement IDs are not supported for this policy type. Update the Sid value."
```

**Resolving the error**

For some policy types, statement IDs must be unique\. The `Sid` \(statement ID\) element allows you to enter an optional identifier that you provide for the policy statement\. You can assign a statement ID value to each statement in a statement array using the `SID` element\. In services that let you specify an ID element, such as SQS and SNS, the `Sid` value is just a sub\-ID of the policy document's ID\. For example, in IAM, the `Sid` value must be unique within a JSON policy\.

**Related terms**
+ [IAM JSON policy elements: Sid](reference_policies_elements_sid.md)

## Error – Unsupported action in policy<a name="access-analyzer-reference-policy-checks-error-unsupported-action-in-policy"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported action in policy: The action {{action}} is not supported for the resource-based policy attached to the resource type {{resourceType}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The action {{action}} is not supported for the resource-based policy attached to the resource type {{resourceType}}."
```

**Resolving the error**

Some actions aren't supported in the `Action` element in the resource\-based policy attached to a different resource type\. For example, AWS Key Management Service actions aren't supported in Amazon S3 bucket policies\. Specify an action that is supported by resource type attached to your resource\-based policy\.

**Related terms**
+ [JSON policy elements: Action](reference_policies_elements_action.md)

## Error – Unsupported element combination<a name="access-analyzer-reference-policy-checks-error-unsupported-element-combination"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported element combination: The policy elements ${element1} and ${element2} can not be used in the same statement. Remove one of these elements.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The policy elements ${element1} and ${element2} can not be used in the same statement. Remove one of these elements."
```

**Resolving the error**

Some combinations of JSON policy elements can't be used together\. For example, you cannot use both `Action` and `NotAction` in the same policy statement\. Other pairs that are mutually exclusive include `Principal/NotPrincipal` and `Resource/NotResource`\.

**Related terms**
+ [IAM JSON policy elements reference](reference_policies_elements.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Error – Unsupported global condition key<a name="access-analyzer-reference-policy-checks-error-unsupported-global-condition-key"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported global condition key: The condition key aws:ARN is not supported. Use aws:PrincipalArn or aws:SourceArn instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition key aws:ARN is not supported. Use aws:PrincipalArn or aws:SourceArn instead."
```

**Resolving the error**

AWS does not support using the specified global condition key\. Depending on your use case, you can use the `aws:PrincipalArn` or `aws:SourceArn` global condition keys\. For example, instead of `aws:ARN`, use the `aws:PrincipalArn` to compare the Amazon Resource Name \(ARN\) of the principal that made the request with the ARN that you specify in the policy\. Alternatively, use the `aws:SourceArn` global condition key to compare the Amazon Resource Name \(ARN\) of the resource making a service\-to\-service request with the ARN that you specify in the policy\.

**Related terms**
+ [AWS global condition context keys](reference_policies_condition-keys.md)

## Error – Unsupported principal<a name="access-analyzer-reference-policy-checks-error-unsupported-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported principal: The policy type ${policy_type} does not support the Principal element. Remove the Principal element.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The policy type ${policy_type} does not support the Principal element. Remove the Principal element."
```

**Resolving the error**

The `Principal` element specifies the principal that is allowed or denied access to a resource\. You cannot use the `Principal` element in an IAM identity\-based policy\. You can use it in the trust policies for IAM roles and in resource\-based policies\. Resource\-based policies are policies that you embed directly in a resource\. For example, you can embed policies in an Amazon S3 bucket or an AWS KMS key\.

**Related terms**
+ [AWS JSON policy elements: Principal](reference_policies_elements_principal.md)
+ [How IAM roles differ from resource\-based policies](id_roles_compare-resource-policies.md)

## Error – Unsupported resource ARN in policy<a name="access-analyzer-reference-policy-checks-error-unsupported-resource-arn-in-policy"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported resource ARN in policy: The resource ARN is not supported for the resource-based policy attached to the resource type {{resourceType}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The resource ARN is not supported for the resource-based policy attached to the resource type {{resourceType}}."
```

**Resolving the error**

Some resource ARNs aren't supported in the `Resource` element of the resource\-based policy when the policy is attached to a different resource type\. For example, AWS KMS ARNs aren't supported in the `Resource` element for Amazon S3 bucket policies\. Specify a resource ARN that is supported by a resource type attached to your resource\-based policy\.

**Related terms**
+ [JSON policy elements: Action](reference_policies_elements_action.md)

## Error – Unsupported Sid<a name="access-analyzer-reference-policy-checks-error-unsupported-sid"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported Sid: Update the characters in the Sid element to use one of the following character types: [a-z, A-Z, 0-9]
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Update the characters in the Sid element to use one of the following character types: [a-z, A-Z, 0-9]"
```

**Resolving the error**

The `Sid` element supports uppercase letters, lowercase letters, and numbers\.

**Related terms**
+ [IAM JSON policy elements: Sid](reference_policies_elements_sid.md)

## Error – Unsupported wildcard in principal<a name="access-analyzer-reference-policy-checks-error-unsupported-wildcard-in-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported wildcard in principal: Wildcards (*, ?) are not supported with the principal key {{principal_key}}. Replace the wildcard with a valid principal value.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Wildcards (*, ?) are not supported with the principal key {{principal_key}}. Replace the wildcard with a valid principal value."
```

**Resolving the error**

The `Principal` element structure supports using a key\-value pair\. The principal value specified in the policy includes a wildcard \(\*\)\. You can't include a wildcard with the principal key that you specified\. For example, when you specify users in a `Principal` element, you cannot use a wildcard to mean "all users"\. You must name a specific user or users\. Similarly, when you specify an assumed\-role session, you cannot use a wildcard to mean "all sessions"\. You must name a specific session\. You also cannot use a wildcard to match part of a name or an ARN\.

To resolve this finding, remove the wildcard and provide a more specific principal\.

**Related terms**
+ [AWS JSON policy elements: Principal](reference_policies_elements_principal.md)

## Error – Missing brace in variable<a name="access-analyzer-reference-policy-checks-error-missing-brace-in-variable"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing brace in variable: The policy variable is missing a closing curly brace. Add } after the variable text.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The policy variable is missing a closing curly brace. Add } after the variable text."
```

**Resolving the error**

Policy variable structure supports using a `$` prefix followed by a pair of curly braces \(`{ }`\)\. Inside the `${ }` characters, include the name of the value from the request that you want to use in the policy\.

To resolve this finding, add the missing brace to make sure the full opening and closing set of braces is present\.

**Related terms**
+ [IAM policy elements: Variables](reference_policies_variables.md)

## Error – Missing quote in variable<a name="access-analyzer-reference-policy-checks-error-missing-quote-in-variable"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing quote in variable: The policy variable default value must begin and end with a single quote. Add the missing quote.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The policy variable default value must begin and end with a single quote. Add the missing quote."
```

**Resolving the error**

When you add a variable to your policy, you can specify a default value for the variable\. If a variable is not present, AWS uses the default text that you provide\.

To add a default value to a variable, surround the default value with single quotes \(`' '`\), and separate the variable text and the default value with a comma and space \(`, `\)\.

For example, if a principal is tagged with `team=yellow`, they can access the `DOC-EXAMPLE-BUCKET` Amazon S3 bucket with the name `DOC-EXAMPLE-BUCKET-yellow`\. A policy with this resource might allow team members to access their own resources, but not those of other teams\. For users without team tags, you might set a default value of `company-wide`\. These users can access only the `DOC-EXAMPLE-BUCKET-company-wide` bucket where they can view broad information, such as instructions for joining a team\.

```
"Resource":"arn:aws:s3:::DOC-EXAMPLE-BUCKET-${aws:PrincipalTag/team, 'company-wide'}"
```

**Related terms**
+ [IAM policy elements: Variables](reference_policies_variables.md)

## Error – Unsupported space in variable<a name="access-analyzer-reference-policy-checks-error-unsupported-space-in-variable"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported space in variable: A space is not supported within the policy variable text. Remove the space.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "A space is not supported within the policy variable text. Remove the space."
```

**Resolving the error**

Policy variable structure supports using a `$` prefix followed by a pair of curly braces \(`{ }`\)\. Inside the `${ }` characters, include the name of the value from the request that you want to use in the policy\. Although you can include a space when you specify a default variable, you cannot include a space in the variable name\.

**Related terms**
+ [IAM policy elements: Variables](reference_policies_variables.md)

## Error – Empty variable<a name="access-analyzer-reference-policy-checks-error-empty-variable"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty variable: Empty policy variable. Remove the ${ } variable structure or provide a variable within the structure.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Empty policy variable. Remove the ${ } variable structure or provide a variable within the structure."
```

**Resolving the error**

Policy variable structure supports using a `$` prefix followed by a pair of curly braces \(`{ }`\)\. Inside the `${ }` characters, include the name of the value from the request that you want to use in the policy\.

**Related terms**
+ [IAM policy elements: Variables](reference_policies_variables.md)

## Error – Variable unsupported in element<a name="access-analyzer-reference-policy-checks-error-variable-unsupported-in-element"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Variable unsupported in element: Policy variables are supported in the Resource and Condition elements. Remove the policy variable {{variable}} from this element.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Policy variables are supported in the Resource and Condition elements. Remove the policy variable {{variable}} from this element."
```

**Resolving the error**

You can use policy variables in the `Resource` element and in string comparisons in the `Condition` element\.

**Related terms**
+ [IAM policy elements: Variables](reference_policies_variables.md)

## Error – Variable unsupported in version<a name="access-analyzer-reference-policy-checks-error-variable-unsupported-in-version"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Variable unsupported in version: To include variables in your policy, use the policy version 2012-10-17 or later.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "To include variables in your policy, use the policy version 2012-10-17 or later."
```

**Resolving the error**

To use policy variables, you must include the `Version` element and set it to a version that supports policy variables\. Variables were introduced in version `2012-10-17`\. Earlier versions of the policy language don't support policy variables\. If you don't set the `Version` to `2012-10-17` or later, variables like `${aws:username}` are treated as literal strings in the policy\.

A `Version` policy element is different from a policy version\. The `Version` policy element is used within a policy and defines the version of the policy language\. A policy version, is created when you change a customer managed policy in IAM\. The changed policy doesn't overwrite the existing policy\. Instead, IAM creates a new version of the managed policy\.

**Related terms**
+ [IAM policy elements: Variables](reference_policies_variables.md)
+ [IAM JSON policy elements: Version](reference_policies_elements_version.md)

## Error – Private IP address<a name="access-analyzer-reference-policy-checks-error-private-ip-address"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Private IP address: aws:SourceIp works only for public IP address ranges. The values for condition key aws:SourceIp include only private IP addresses and will not have the desired effect. Update the value to include only public IP addresses.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "aws:SourceIp works only for public IP address ranges. The values for condition key aws:SourceIp include only private IP addresses and will not have the desired effect. Update the value to include only public IP addresses."
```

**Resolving the error**

The global condition key `aws:SourceIp` works only for public IP address ranges\. You receive this error when your policy allows only private IP addresses\. In this case, the condition would never match\.
+ [aws:SourceIp global condition key](reference_policies_condition-keys.md#condition-keys-sourceip)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Error – Private NotIpAddress<a name="access-analyzer-reference-policy-checks-error-private-not-ip-address"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Private NotIpAddress: The values for condition key aws:SourceIp include only private IP addresses and has no effect. aws:SourceIp works only for public IP address ranges. Update the value to include only public IP addresses.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The values for condition key aws:SourceIp include only private IP addresses and has no effect. aws:SourceIp works only for public IP address ranges. Update the value to include only public IP addresses."
```

**Resolving the error**

The global condition key `aws:SourceIp` works only for public IP address ranges\. You receive this error when you use the `NotIpAddress` condition operator and list only private IP addresses\. In this case, the condition would always match and would be ineffective\.
+ [aws:SourceIp global condition key](reference_policies_condition-keys.md#condition-keys-sourceip)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Error – Policy size exceeds SCP quota<a name="access-analyzer-reference-policy-checks-error-policy-size-exceeds-scp-quota"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Policy size exceeds SCP quota: The {{policySize}} characters in the service control policy (SCP) exceed the {{policySizeQuota}} character maximum for SCPs. We recommend that you use multiple granular policies.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The {{policySize}} characters in the service control policy (SCP) exceed the {{policySizeQuota}} character maximum for SCPs. We recommend that you use multiple granular policies."
```

**Resolving the error**

AWS Organizations service control policies \(SCPs\) support specifying values in the `Action` or `NotAction` elements\. However, these values can include wildcards \(\*\) only at the end of the string\. This means that you can specify `iam:Get*` but not `iam:*role`\.

To specify multiple actions, AWS recommends that you list them individually\.

**Related terms**
+ [Quotas for AWS Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_reference_limits.html)
+ [AWS Organizations service control policies](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)

## Error – Invalid service principal format<a name="access-analyzer-reference-policy-checks-error-invalid-service-principal-format"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid service principal format: The service principal does not match the expected format. Use the format {{expectedFormat}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The service principal does not match the expected format. Use the format {{expectedFormat}}."
```

**Resolving the error**

The value in the condition key\-value pair must match a defined service principal format\.

A *service principal* is an identifier that is used to grant permissions to a service\. You can specify a service principal in the `Principal` element or as a value for some global condition keys and service\-specific keys\. The service principal is defined by each service\.

The identifier for a service principal includes the service name, and is usually in the following format in all lowercase letters:

`service-name.amazonaws.com`

Some service\-specific keys may use a different format for service principals\. For example, the `kms:ViaService` condition key requires the following format for service principals in all lowercase letters:

`service-name.AWS_region.amazonaws.com`

**Related terms**
+ [Service principals](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-services)
+ [AWS global condition keys](reference_policies_condition-keys.md)
+ [`kms:ViaService` condition key](https://docs.aws.amazon.com/kms/latest/developerguide/policy-conditions.html#conditions-kms-via-service)

## Error – Missing tag key in condition<a name="access-analyzer-reference-policy-checks-error-missing-tag-key-in-condition"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing tag key in condition: The condition key {{conditionKeyName}} must include a tag key to control access based on tags. Use the format {{conditionKeyName}}tag-key and specify a key name for tag-key.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition key {{conditionKeyName}} must include a tag key to control access based on tags. Use the format {{conditionKeyName}}tag-key and specify a key name for tag-key."
```

**Resolving the error**

To control access based on tags, you provide tag information in the [condition element](reference_policies_elements_condition.md) of a policy\.

For example, to [control access to AWS resources](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_tags.html#access_tags_control-resources), you include the `aws:ResourceTag` condition key\. This key requires the format `aws:ResourceTag/tag-key`\. To specify the tag key `owner` and the tag value `JaneDoe` in a condition, use the following format\.

```
"Condition": {
    "StringEquals": {"aws:ResourceTag/owner": "JaneDoe"}
}
```

**Related terms**
+ [Controlling access using tags](access_iam-tags.md)
+ [Conditions](reference_policies_elements_condition.md)
+ [Global condition keys](reference_policies_condition-keys.md)
+ [AWS service condition keys](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html)

## Error – Invalid vpc format<a name="access-analyzer-reference-policy-checks-error-invalid-vpc-format"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid vpc format: The VPC identifier in the condition key value is not valid. Use the prefix 'vpc-' followed by 8 or 17 alphanumeric characters.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The VPC identifier in the condition key value is not valid. Use the prefix 'vpc-' followed by 8 or 17 alphanumeric characters."
```

**Resolving the error**

The `aws:SourceVpc` condition key must use the prefix `vpc-` followed by either 8 or 17 alphanumeric characters, for example, `vpc-11223344556677889` or `vpc-12345678`\.

**Related terms**
+ [AWS global condition keys: aws:SourceVpc](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcevpc)

## Error – Invalid vpce format<a name="access-analyzer-reference-policy-checks-error-invalid-vpce-format"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid vpce format: The VPCE identifier in the condition key value is not valid.  Use the prefix 'vpce-' followed by 8 or 17 alphanumeric characters.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The VPCE identifier in the condition key value is not valid.  Use the prefix 'vpce-' followed by 8 or 17 alphanumeric characters."
```

**Resolving the error**

The `aws:SourceVpce` condition key must use the prefix `vpce-` followed by either 8 or 17 alphanumeric characters, for example, `vpce-11223344556677889` or `vpce-12345678`\.

**Related terms**
+ [AWS global condition keys: aws:SourceVpce](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcevpce)

## Error – Federated principal not supported<a name="access-analyzer-reference-policy-checks-error-federated-principal-not-supported"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Federated principal not supported: The policy type does not support a federated identity provider in the principal element. Use a supported principal.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The policy type does not support a federated identity provider in the principal element. Use a supported principal."
```

**Resolving the error**

The `Principal` element uses federated principals for trust policies attached to IAM roles to provide access through identity federation\. Identity policies and other resource\-based policies don't support a federated identity provider in the `Principal` element\. For example, you can't use a SAML principal in an Amazon S3 bucket policy\. Change the `Principal` element to a supported principal type\.

**Related terms**
+ [Creating a role for identity federation](id_roles_create_for-idp.md)
+ [JSON policy elements: Principal](reference_policies_elements_principal.md)

## Error – Unsupported action for condition key<a name="access-analyzer-reference-policy-checks-error-unsupported-action-for-condition-key"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported action for condition key: The following actions: {{actions}} are not supported by the condition key {{key}}. The condition will not be evaluated for these actions. We recommend that you move these actions to a different statement without this condition key.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The following actions: {{actions}} are not supported by the condition key {{key}}. The condition will not be evaluated for these actions. We recommend that you move these actions to a different statement without this condition key."
```

**Resolving the error**

Make sure that the condition key in the `Condition` element of the policy statement applies to every action in the `Action` element\. To ensure that the actions you specify are effectively allowed or denied by your policy, you should move the unsupported actions to a different statement without the condition key\.

**Note**  
If the `Action` element has actions with wildcards, IAM Access Analyzer doesn't evaluate those actions for this error\.

**Related terms**
+ [JSON policy elements: Action](reference_policies_elements_action.md)

## Error – Unsupported action in policy<a name="access-analyzer-reference-policy-checks-error-unsupported-action-in-policy"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported action in policy: The action {{action}} is not supported for the resource-based policy attached to the resource type {{resourceType}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The action {{action}} is not supported for the resource-based policy attached to the resource type {{resourceType}}."
```

**Resolving the error**

Some actions aren't supported in the `Action` element in the resource\-based policy attached to a different resource type\. For example, AWS Key Management Service actions aren't supported in Amazon S3 bucket policies\. Specify an action that is supported by resource type attached to your resource\-based policy\.

**Related terms**
+ [JSON policy elements: Action](reference_policies_elements_action.md)

## Error – Unsupported resource ARN in policy<a name="access-analyzer-reference-policy-checks-error-unsupported-resource-arn-in-policy"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported resource ARN in policy: The resource ARN is not supported for the resource-based policy attached to the resource type {{resourceType}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The resource ARN is not supported for the resource-based policy attached to the resource type {{resourceType}}."
```

**Resolving the error**

Some resource ARNs aren't supported in the `Resource` element of the resource\-based policy when the policy is attached to a different resource type\. For example, AWS KMS ARNs aren't supported in the `Resource` element for Amazon S3 bucket policies\. Specify a resource ARN that is supported by a resource type attached to your resource\-based policy\.

**Related terms**
+ [JSON policy elements: Action](reference_policies_elements_action.md)

## Error – Unsupported condition key for service principal<a name="access-analyzer-reference-policy-checks-error-unsupported-condition-key-for-service-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unsupported condition key for service principal: The following condition keys are not supported when used with the service principal: {{conditionKeys}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The following condition keys are not supported when used with the service principal: {{conditionKeys}}."
```

**Resolving the error**

You can specify AWS services in the `Principal` element of a resource\-based policy using a *service principal*, which is an identifier for the service\. You can't use some condition keys with certain service principals\. For example, you can't use the `aws:PrincipalOrgID` condition key with the service principal `cloudfront.amazonaws.com`\. You should remove condition keys that do not apply to the service principal in the `Principal` element\.

**Related terms**
+ [Service principals](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-services)
+ [JSON policy elements: Principal](reference_policies_elements_principal.md)

## Error – Role trust policy syntax error notprincipal<a name="access-analyzer-reference-policy-checks-error-role-trust-policy-syntax-error-notprincipal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Role trust policy syntax error notprincipal: Role trust policies do not support NotPrincipal. Update the policy to use a Principal element instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Role trust policies do not support NotPrincipal. Update the policy to use a Principal element instead."
```

**Resolving the error**

A role trust policy is a resource\-based policy that is attached to an IAM role\. Trust policies define which principal entities \(accounts, users, roles, and federated users\) can assume the role\. Role trust policies do not support `NotPrincipal`\. Update the policy to use a `Principal` element instead\.

**Related terms**
+ [JSON policy elements: Principal](reference_policies_elements_principal.md)
+ [JSON policy elements: NotPrincipal](reference_policies_elements_notprincipal.md)

## Error – Role trust policy unsupported wildcard in principal<a name="access-analyzer-reference-policy-checks-error-role-trust-policy-unsupported-wildcard-in-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Role trust policy unsupported wildcard in principal: "Principal:" "*" is not supported in the principal element of a role trust policy. Replace the wildcard with a valid principal value.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": ""Principal:" "*" is not supported in the principal element of a role trust policy. Replace the wildcard with a valid principal value."
```

**Resolving the error**

A role trust policy is a resource\-based policy that is attached to an IAM role\. Trust policies define which principal entities \(accounts, users, roles, and federated users\) can assume the role\. `"Principal:" "*"` is not supported in the `Principal` element of a role trust policy\. Replace the wildcard with a valid principal value\.

**Related terms**
+ [JSON policy elements: Principal](reference_policies_elements_principal.md)

## Error – Role trust policy syntax error resource<a name="access-analyzer-reference-policy-checks-error-role-trust-policy-syntax-error-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Role trust policy syntax error resource: Role trust policies apply to the role that they are attached to. You cannot specify a resource. Remove the Resource or NotResource element.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Role trust policies apply to the role that they are attached to. You cannot specify a resource. Remove the Resource or NotResource element."
```

**Resolving the error**

A role trust policy is a resource\-based policy that is attached to an IAM role\. Trust policies define which principal entities \(accounts, users, roles, and federated users\) can assume the role\. Role trust policies apply to the role that they are attached to\. You cannot specify a `Resource` or `NotResource` element in a role trust policy\. Remove the `Resource` or `NotResource` element\.
+ [JSON policy elements: Resource](reference_policies_elements_resource.md)
+ [JSON policy elements: NotResource](reference_policies_elements_notresource.md)

## Error – Missing action for condition key<a name="access-analyzer-reference-policy-checks-error-missing-action-for-condition-key"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing action for condition key: The {{actionName}} action must be in the action block to allow setting values for the condition key {{keyName}}. Add {{actionName}} to the action block.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The {{actionName}} action must be in the action block to allow setting values for the condition key {{keyName}}. Add {{actionName}} to the action block."
```

**Resolving the error**

The condition key in the `Condition` element of the policy statement is not evaluated unless the specified action is in the `Action` element\. To ensure that the condition keys you specify are effectively allowed or denied by your policy, add the action to the `Action` element\.

**Related terms**
+ [JSON policy elements: Action](reference_policies_elements_action.md)

## Error – Invalid federated principal syntax in role trust policy<a name="access-analyzer-reference-policy-checks-error-invalid-federated-principal-syntax-in-role-trust-policy"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid federated principal syntax in role trust policy: The principal value specifies a federated principal that does not match the expected format. Update the federated principal to a domain name or a SAML metadata ARN.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The principal value specifies a federated principal that does not match the expected format. Update the federated principal to a domain name or a SAML metadata ARN."
```

**Resolving the error**

The principal value specifies a federated principal that does not match the expected format\. Update the format of the federated principal to a valid domain name or a SAML metadata ARN\.

**Related terms**
+ [Federated users and roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction_access-management.html#intro-access-roles)

## Error – Mismatched action for principal<a name="access-analyzer-reference-policy-checks-error-mismatched-action-for-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Mismatched action for principal: The {{actionName}} action is invalid with the following principal(s): {{principalNames}}. Use a SAML provider principal with the sts:AssumeRoleWithSAML action or use an OIDC provider principal with the sts:AssumeRoleWithWebIdentity action. Ensure the provider is Federated if you use either of the two options.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The {{actionName}} action is invalid with the following principal(s): {{principalNames}}. Use a SAML provider principal with the sts:AssumeRoleWithSAML action or use an OIDC provider principal with the sts:AssumeRoleWithWebIdentity action. Ensure the provider is Federated if you use either of the two options."
```

**Resolving the error**

The action specified in the `Action` element of the policy statement is invalid with the principal specified in the `Principal` element\. For example, you can't use a SAML provider principal with the `sts:AssumeRoleWithWebIdentity` action\. You should use a SAML provider principal with the `sts:AssumeRoleWithSAML` action or use an OIDC provider principal with the `sts:AssumeRoleWithWebIdentity` action\.

**Related terms**
+ [AssumeRoleWithSAML](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRoleWithSAML.html)
+ [AssumeRoleWithWebIdentity](https://docs.aws.amazon.com/STS/latest/APIReference/API_AssumeRoleWithWebIdentity.html)

## Error – Missing action for roles anywhere trust policy<a name="access-analyzer-reference-policy-checks-error-missing-action-for-roles-anywhere-trust-policy"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing action for roles anywhere trust policy: The rolesanywhere.amazonaws.com service principal requires the sts:AssumeRole, sts:SetSourceIdentity, and sts:TagSession permissions to assume a role. Add the missing permissions to the policy.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The rolesanywhere.amazonaws.com service principal requires the sts:AssumeRole, sts:SetSourceIdentity, and sts:TagSession permissions to assume a role. Add the missing permissions to the policy."
```

**Resolving the error**

For IAM Roles Anywhere to be able to assume a role and deliver temporary AWS credentials, the role must trust the IAM Roles Anywhere service principal\. The IAM Roles Anywhere service principal requires the `sts:AssumeRole`, `sts:SetSourceIdentity`, and `sts:TagSession` permissions to assume a role\. If any of the permissions are missing, you must add them to your policy\.

**Related terms**
+ [Trust model in AWS Identity and Access Management Roles Anywhere](https://docs.aws.amazon.com/rolesanywhere/latest/userguide/trust-model.html)

## General Warning – Create SLR with NotResource<a name="access-analyzer-reference-policy-checks-general-warning-create-slr-with-not-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Create SLR with NotResource: Using the iam:CreateServiceLinkedRole action with NotResource can allow creation of unintended service-linked roles for multiple resources. We recommend that you specify resource ARNs instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using the iam:CreateServiceLinkedRole action with NotResource can allow creation of unintended service-linked roles for multiple resources. We recommend that you specify resource ARNs instead."
```

**Resolving the general warning**

The action `iam:CreateServiceLinkedRole` grants permission to create an IAM role that allows an AWS service to perform actions on your behalf\. Using `iam:CreateServiceLinkedRole` in a policy with the `NotResource` element can allow creating unintended service\-linked roles for multiple resources\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\.
+ [CreateServiceLinkedRole operation](https://docs.aws.amazon.com/IAM/latest/APIReference/API_CreateServiceLinkedRole.html)
+ [IAM JSON policy elements: NotResource](reference_policies_elements_notresource.md)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## General Warning – Create SLR with star in action and NotResource<a name="access-analyzer-reference-policy-checks-general-warning-create-slr-with-star-in-action-and-not-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Create SLR with star in action and NotResource: Using an action with a wildcard(*) and NotResource can allow creation of unintended service-linked roles because it can allow iam:CreateServiceLinkedRole permissions on multiple resources. We recommend that you specify resource ARNs instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using an action with a wildcard(*) and NotResource can allow creation of unintended service-linked roles because it can allow iam:CreateServiceLinkedRole permissions on multiple resources. We recommend that you specify resource ARNs instead."
```

**Resolving the general warning**

The action `iam:CreateServiceLinkedRole` grants permission to create an IAM role that allows an AWS service to perform actions on your behalf\. Policies with a wildcard \(\*\) in the `Action` and that include the `NotResource` element can allow creation of unintended service\-linked roles for multiple resources\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\.
+ [CreateServiceLinkedRole operation](https://docs.aws.amazon.com/IAM/latest/APIReference/API_CreateServiceLinkedRole.html)
+ [IAM JSON policy elements: NotResource](reference_policies_elements_notresource.md)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## General Warning – Create SLR with NotAction and NotResource<a name="access-analyzer-reference-policy-checks-general-warning-create-slr-with-not-action-and-not-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Create SLR with NotAction and NotResource: Using NotAction with NotResource can allow creation of unintended service-linked roles because it allows iam:CreateServiceLinkedRole permissions on multiple resources. We recommend that you specify resource ARNs instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using NotAction with NotResource can allow creation of unintended service-linked roles because it allows iam:CreateServiceLinkedRole permissions on multiple resources. We recommend that you specify resource ARNs instead."
```

**Resolving the general warning**

The action `iam:CreateServiceLinkedRole` grants permission to create an IAM role that allows an AWS service to perform actions on your behalf\. Using the `NotAction` element with the `NotResource` element can allow creating unintended service\-linked roles for multiple resources\. AWS recommends that you rewrite the policy to allow `iam:CreateServiceLinkedRole` on a limited list of ARNs in the `Resource` element instead\. You can also add `iam:CreateServiceLinkedRole` to the `NotAction` element\.
+ [CreateServiceLinkedRole operation](https://docs.aws.amazon.com/IAM/latest/APIReference/API_CreateServiceLinkedRole.html)
+ [IAM JSON policy elements: NotAction](reference_policies_elements_notaction.md)
+ [IAM JSON policy elements: Action](reference_policies_elements_action.md)
+ [IAM JSON policy elements: NotResource](reference_policies_elements_notresource.md)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## General Warning – Create SLR with star in resource<a name="access-analyzer-reference-policy-checks-general-warning-create-slr-with-star-in-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Create SLR with star in resource: Using the iam:CreateServiceLinkedRole action with wildcards (*) in the resource can allow creation of unintended service-linked roles. We recommend that you specify resource ARNs instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using the iam:CreateServiceLinkedRole action with wildcards (*) in the resource can allow creation of unintended service-linked roles. We recommend that you specify resource ARNs instead."
```

**Resolving the general warning**

The action `iam:CreateServiceLinkedRole` grants permission to create an IAM role that allows an AWS service to perform actions on your behalf\. Using `iam:CreateServiceLinkedRole` in a policy with a wildcard \(\*\) in the `Resource` element can allow creating unintended service\-linked roles for multiple resources\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\.
+ [CreateServiceLinkedRole operation](https://docs.aws.amazon.com/IAM/latest/APIReference/API_CreateServiceLinkedRole.html)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

### AWS managed policies with this general warning<a name="accan-ref-policy-check-message-fix-general-warning-create-slr-with-star-in-resource-awsmanpol"></a>

[AWS managed policies](access_policies_managed-vs-inline.md#aws-managed-policies) enable you to get started with AWS by assigning permissions based on general AWS use cases\.

Some of those use cases are for power users within your account\. The following AWS managed policies provide power user access and grant permissions to create [service\-linked roles](using-service-linked-roles.md) for any AWS service\. AWS recommends that you attach the following AWS managed policies to only IAM identities that you consider power users\.
+ [PowerUserAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/PowerUserAccess)
+ [AlexaForBusinessFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AlexaForBusinessFullAccess)
+ [AWSOrganizationsServiceTrustPolicy](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AWSOrganizationsServiceTrustPolicy) – This AWS managed policy provides permissions for use by the AWS Organizations service\-linked role\. This role allows Organizations to create additional service\-linked roles for other services in your AWS organization\.

## General Warning – Create SLR with star in action and resource<a name="access-analyzer-reference-policy-checks-general-warning-create-slr-with-star-in-action-and-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Create SLR with star in action and resource: Using wildcards (*) in the action and the resource can allow creation of unintended service-linked roles because it allows iam:CreateServiceLinkedRole permissions on all resources. We recommend that you specify resource ARNs instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using wildcards (*) in the action and the resource can allow creation of unintended service-linked roles because it allows iam:CreateServiceLinkedRole permissions on all resources. We recommend that you specify resource ARNs instead."
```

**Resolving the general warning**

The action `iam:CreateServiceLinkedRole` grants permission to create an IAM role that allows an AWS service to perform actions on your behalf\. Policies with a wildcard \(\*\) in the `Action` and `Resource` elements can allow creating unintended service\-linked roles for multiple resources\. This allows creating a service\-linked role when you specify `"Action": "*"`, `"Action": "iam:*"`, or `"Action": "iam:Create*"`\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\.
+ [CreateServiceLinkedRole operation](https://docs.aws.amazon.com/IAM/latest/APIReference/API_CreateServiceLinkedRole.html)
+ [IAM JSON policy elements: Action](reference_policies_elements_action.md)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

### AWS managed policies with this general warning<a name="accan-ref-policy-check-message-fix-general-warning-create-slr-with-star-in-action-and-resource-awsmanpol"></a>

[AWS managed policies](access_policies_managed-vs-inline.md#aws-managed-policies) enable you to get started with AWS by assigning permissions based on general AWS use cases\.

Some of those use cases are for administrators within your account\. The following AWS managed policies provide administrator access and grant permissions to create [service\-linked roles](using-service-linked-roles.md) for any AWS service\. AWS recommends that you attach the following AWS managed policies to only the IAM identities that you consider administrators\.
+ [AdministratorAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AdministratorAccess)
+ [IAMFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/IAMFullAccess)

## General Warning – Create SLR with star in resource and NotAction<a name="access-analyzer-reference-policy-checks-general-warning-create-slr-with-star-in-resource-and-not-action"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Create SLR with star in resource and NotAction: Using a resource with wildcards (*) and NotAction can allow creation of unintended service-linked roles because it allows iam:CreateServiceLinkedRole permissions on all resources. We recommend that you specify resource ARNs instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using a resource with wildcards (*) and NotAction can allow creation of unintended service-linked roles because it allows iam:CreateServiceLinkedRole permissions on all resources. We recommend that you specify resource ARNs instead."
```

**Resolving the general warning**

The action `iam:CreateServiceLinkedRole` grants permission to create an IAM role that allows an AWS service to perform actions on your behalf\. Using the `NotAction` element in a policy with a wildcard \(\*\) in the `Resource` element can allow creating unintended service\-linked roles for multiple resources\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\. You can also add `iam:CreateServiceLinkedRole` to the `NotAction` element\.
+ [CreateServiceLinkedRole operation](https://docs.aws.amazon.com/IAM/latest/APIReference/API_CreateServiceLinkedRole.html)
+ [IAM JSON policy elements: NotAction](reference_policies_elements_notaction.md)
+ [IAM JSON policy elements: Action](reference_policies_elements_action.md)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## General Warning – Deprecated global condition key<a name="access-analyzer-reference-policy-checks-general-warning-deprecated-global-condition-key"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Deprecated global condition key: We recommend that you update aws:ARN to use the newer condition key aws:PrincipalArn.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "We recommend that you update aws:ARN to use the newer condition key aws:PrincipalArn."
```

**Resolving the general warning**

The policy includes a deprecated global condition key\. Update the condition key in the condition key\-value pair to use a supported global condition key\.
+ [Global condition keys](reference_policies_condition-keys.md)

## General Warning – Invalid date value<a name="access-analyzer-reference-policy-checks-general-warning-invalid-date-value"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid date value: The date {{date}} might not resolve as expected. We recommend that you use the YYYY-MM-DD format.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The date {{date}} might not resolve as expected. We recommend that you use the YYYY-MM-DD format."
```

**Resolving the general warning**

Unix Epoch time describes a point in time that has elapsed since January 1, 1970, minus leap seconds\. Epoch time might not resolve to the precise time that you expect\. AWS recommends that you use the W3C standard for date and time formats\. For example, you could specify a complete date, such as YYYY\-MM\-DD \(1997\-07\-16\), or you could also append the time to the second, such as YYYY\-MM\-DDThh:mm:ssTZD \(1997\-07\-16T19:20:30\+01:00\)\.
+ [W3C Date and Time Formats](https://www.w3.org/TR/NOTE-datetime)
+ [IAM JSON policy elements: Version](reference_policies_elements_version.md)
+ [aws:CurrentTime global condition key](reference_policies_condition-keys.md#condition-keys-currenttime)

## General Warning – Invalid role reference<a name="access-analyzer-reference-policy-checks-general-warning-invalid-role-reference"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid role reference: The Principal element includes the IAM role ID {{roleid}}. We recommend that you use a role ARN instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The Principal element includes the IAM role ID {{roleid}}. We recommend that you use a role ARN instead."
```

**Resolving the general warning**

AWS recommends that you specify the Amazon Resource Name \(ARN\) for an IAM role instead of its principal ID\. When IAM saves the policy, it will transform the ARN into the principal ID for the existing role\. AWS includes a safety precaution\. If someone deletes and recreates the role, it will have a new ID, and the policy won't match the new role's ID\. 
+ [Specifying a principal: IAM roles](reference_policies_elements_principal.md#principal-roles)
+ [IAM ARNs](reference_identifiers.md#identifiers-arns)
+ [IAM unique IDs](reference_identifiers.md#identifiers-unique-ids)

## General Warning – Invalid user reference<a name="access-analyzer-reference-policy-checks-general-warning-invalid-user-reference"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Invalid user reference: The Principal element includes the IAM user ID {{userid}}. We recommend that you use a user ARN instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The Principal element includes the IAM user ID {{userid}}. We recommend that you use a user ARN instead."
```

**Resolving the general warning**

AWS recommends that you specify the Amazon Resource Name \(ARN\) for an IAM user instead of its principal ID\. When IAM saves the policy, it will transform the ARN into the principal ID for the existing user\. AWS includes a safety precaution\. If someone deletes and recreates the user, it will have a new ID, and the policy won't match the new user's ID\. 
+ [Specifying a principal: IAM users](reference_policies_elements_principal.md#principal-users)
+ [IAM ARNs](reference_identifiers.md#identifiers-arns)
+ [IAM unique IDs](reference_identifiers.md#identifiers-unique-ids)

## General Warning – Missing version<a name="access-analyzer-reference-policy-checks-general-warning-missing-version"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing version: We recommend that you specify the Version element to help you with debugging permission issues.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "We recommend that you specify the Version element to help you with debugging permission issues."
```

**Resolving the general warning**

AWS recommends that you include the optional `Version` parameter in your policy\. If you do not include a Version element, the value defaults to `2012-10-17`, but newer features, such as policy variables, will not work with your policy\. For example, variables such as `${aws:username}` aren't recognized as variables and are instead treated as literal strings in the policy\.
+ [IAM JSON policy elements: Version](reference_policies_elements_version.md)

## General Warning – Unique Sids recommended<a name="access-analyzer-reference-policy-checks-general-warning-unique-sids-recommended"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Unique Sids recommended: We recommend that you use statement IDs that are unique to your policy. Update the Sid value.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "We recommend that you use statement IDs that are unique to your policy. Update the Sid value."
```

**Resolving the general warning**

AWS recommends that you use unique statement IDs\. The `Sid` \(statement ID\) element allows you to enter an optional identifier that you provide for the policy statement\. You can assign a statement ID value to each statement in a statement array using the `SID` element\.

**Related terms**
+ [IAM JSON policy elements: Sid](reference_policies_elements_sid.md)

## General Warning – Wildcard without like operator<a name="access-analyzer-reference-policy-checks-general-warning-wildcard-without-like-operator"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Wildcard without like operator: Your condition value includes a * or ? character. If you meant to use a wildcard (*, ?), update the condition operator to include Like.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Your condition value includes a * or ? character. If you meant to use a wildcard (*, ?), update the condition operator to include Like."
```

**Resolving the general warning**

The `Condition` element structure requires that you use a condition operator and a key\-value pair\. When you specify a condition value that uses a wildcard \(\*, ?\), you must use the `Like` version of the condition operator\. For example, instead of the `StringEquals` string condition operator, use `StringLike`\.

```
"Condition": {"StringLike": {"aws:PrincipalTag/job-category": "admin-*"}}
```
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

### AWS managed policies with this general warning<a name="accan-ref-policy-check-message-fix-general-warning-wildcard-without-like-operator-awsmanpol"></a>

[AWS managed policies](access_policies_managed-vs-inline.md#aws-managed-policies) enable you to get started with AWS by assigning permissions based on general AWS use cases\.

The following AWS managed policies include wildcards in their condition value without a condition operator that includes `Like` for pattern\-matching\. When using the AWS managed policy as a reference to create your customer managed policy, AWS recommends that you use a condition operator that supports pattern\-matching with wildcards \(\*, ?\), such as `StringLike`\.
+ [AWSGlueConsoleSageMakerNotebookFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AWSGlueConsoleSageMakerNotebookFullAccess)

## General Warning – Policy size exceeds identity policy quota<a name="access-analyzer-reference-policy-checks-general-warning-policy-size-exceeds-identity-policy-quota"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Policy size exceeds identity policy quota: The {{policySize}} characters in the identity policy, excluding whitespace, exceed the {{policySizeQuota}} character maximum for inline and managed policies. We recommend that you use multiple granular policies.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The {{policySize}} characters in the identity policy, excluding whitespace, exceed the {{policySizeQuota}} character maximum for inline and managed policies. We recommend that you use multiple granular policies."
```

**Resolving the general warning**

You can attach up to 10 managed policies to an IAM identity \(user, group of users, or role\)\. However, the size of each managed policy cannot exceed the default quota of 6,144 characters\. IAM does not count white space when calculating the size of a policy against this quota\. Quotas, also referred to as limits in AWS, are the maximum values for the resources, actions, and items in your AWS account\.

Additionally, you can add as many inline policies as you want to an IAM identity\. However, the sum size of all inline policies per identity cannot exceed the specified quota\.

If your policy is larger than the quota, you can organize your policy into multiple statements and group the statements into multiple policies\.

**Related terms**
+ [IAM and AWS STS character quotas](reference_iam-quotas.md)
+ [Multiple statements and multiple policies](access_policies.md#policies-syntax-multiples)
+ [IAM customer managed policies](access_policies_managed-vs-inline.md#customer-managed-policies)
+ [Overview of JSON policies](access_policies.md#access_policies-json)
+ [IAM JSON policy grammar](reference_policies_grammar.md)

### AWS managed policies with this general warning<a name="accan-ref-policy-check-message-fix-general-warning-policy-size-exceeds-identity-policy-quota-awsmanpol"></a>

[AWS managed policies](access_policies_managed-vs-inline.md#aws-managed-policies) enable you to get started with AWS by assigning permissions based on general AWS use cases\.

The following AWS managed policies grant permissions to actions across many AWS services and exceed the maximum policy size\. When using the AWS managed policy as a reference to create your managed policy, you must split the policy into multiple policies\.
+ [ReadOnlyAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/ReadOnlyAccess)
+ [AWSSupportServiceRolePolicy](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AWSSupportServiceRolePolicy)

## General Warning – Policy size exceeds resource policy quota<a name="access-analyzer-reference-policy-checks-general-warning-policy-size-exceeds-resource-policy-quota"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Policy size exceeds resource policy quota: The {{policySize}} characters in the resource policy exceed the {{policySizeQuota}} character maximum for resource policies. We recommend that you use multiple granular policies.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The {{policySize}} characters in the resource policy exceed the {{policySizeQuota}} character maximum for resource policies. We recommend that you use multiple granular policies."
```

**Resolving the general warning**

Resource\-based policies are JSON policy documents that you attach to a resource, such as an Amazon S3 bucket\. These policies grant the specified principal permission to perform specific actions on that resource and define under what conditions this applies\. The size of resource\-based policies cannot exceed the quota set for that resource\. Quotas, also referred to as limits in AWS, are the maximum values for the resources, actions, and items in your AWS account\.

If your policy is larger than the quota, you can organize your policy into multiple statements and group the statements into multiple policies\.

**Related terms**
+ [Resource\-based policies](access_policies.md#policies_resource-based)
+ [Amazon S3 bucket policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/bucket-policies.html)
+ [Multiple statements and multiple policies](access_policies.md#policies-syntax-multiples)
+ [Overview of JSON policies](access_policies.md#access_policies-json)
+ [IAM JSON policy grammar](reference_policies_grammar.md)

## General Warning – Type mismatch<a name="access-analyzer-reference-policy-checks-general-warning-type-mismatch"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Type mismatch: Use the operator type {{allowed}} instead of operator {{operator}} for the condition key {{key}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Use the operator type {{allowed}} instead of operator {{operator}} for the condition key {{key}}."
```

**Resolving the general warning**

Update the text to use the supported condition operator data type\.

For example, the `aws:MultiFactorAuthPresent` global condition key requires a condition operator with the `Boolean` data type\. If you provide a date or an integer, the data type won't match\.

**Related terms**
+ [Global condition keys](reference_policies_condition-keys.md)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)

## General Warning – Type mismatch Boolean<a name="access-analyzer-reference-policy-checks-general-warning-type-mismatch-boolean"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Type mismatch Boolean: Add a valid Boolean value (true or false) for the condition operator {{operator}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add a valid Boolean value (true or false) for the condition operator {{operator}}."
```

**Resolving the general warning**

Update the text to use a Boolean condition operator data type, such as `true` or `false`\.

For example, the `aws:MultiFactorAuthPresent` global condition key requires a condition operator with the `Boolean` data type\. If you provide a date or an integer, the data type won't match\.

**Related terms**
+ [Boolean condition operators](reference_policies_elements_condition_operators.md#Conditions_Boolean)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)

## General Warning – Type mismatch date<a name="access-analyzer-reference-policy-checks-general-warning-type-mismatch-date"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Type mismatch date: The date condition operator is used with an invalid value. Specify a valid date using YYYY-MM-DD or other ISO 8601 date/time format.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The date condition operator is used with an invalid value. Specify a valid date using YYYY-MM-DD or other ISO 8601 date/time format."
```

**Resolving the general warning**

Update the text to use the date condition operator data type, in a `YYYY-MM-DD` or other ISO 8601 date time format\.

**Related terms**
+ [Date condition operators](reference_policies_elements_condition_operators.md#Conditions_Date)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)

## General Warning – Type mismatch IP range<a name="access-analyzer-reference-policy-checks-general-warning-type-mismatch-ip-range"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Type mismatch IP range: The condition operator {{operator}} is used with an invalid IP range value. Specify the IP range in standard CIDR format.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition operator {{operator}} is used with an invalid IP range value. Specify the IP range in standard CIDR format."
```

**Resolving the general warning**

Update the text to use the IP address condition operator data type, in a CIDR format\.

**Related terms**
+ [IP address condition operators](reference_policies_elements_condition_operators.md#Conditions_IPAddress)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)

## General Warning – Type mismatch number<a name="access-analyzer-reference-policy-checks-general-warning-type-mismatch-number"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Type mismatch number: Add a valid numeric value for the condition operator {{operator}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add a valid numeric value for the condition operator {{operator}}."
```

**Resolving the general warning**

Update the text to use the numeric condition operator data type\.

**Related terms**
+ [Numeric condition operators](reference_policies_elements_condition_operators.md#Conditions_Numeric)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)

## General Warning – Type mismatch string<a name="access-analyzer-reference-policy-checks-general-warning-type-mismatch-string"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Type mismatch string: Add a valid base64-encoded string value for the condition operator {{operator}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add a valid base64-encoded string value for the condition operator {{operator}}."
```

**Resolving the general warning**

Update the text to use the string condition operator data type\.

**Related terms**
+ [String condition operators](reference_policies_elements_condition_operators.md#Conditions_String)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)

## General Warning – Specific github repo and branch recommended<a name="access-analyzer-reference-policy-checks-general-warning-specific-github-repo-and-branch-recommended"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Specific github repo and branch recommended: Using a wildcard (*) in token.actions.githubusercontent.com:sub can allow requests from more sources than you intended. Specify the value of token.actions.githubusercontent.com:sub with the repository and branch name.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using a wildcard (*) in token.actions.githubusercontent.com:sub can allow requests from more sources than you intended. Specify the value of token.actions.githubusercontent.com:sub with the repository and branch name."
```

**Resolving the general warning**

If you use GitHub as an OIDC IdP, best practice is to limit the entities that can assume the role associated with the IAM IdP\. When you include a `Condition` statement in a role trust policy, you can limit the role to a specific GitHub organization, repository, or branch\. You can use the condition key `token.actions.githubusercontent.com:sub` to limit access\. We recommend that you limit the condition to a specific set of repositories or branches\. If you use a wildcard \(`*`\) in `token.actions.githubusercontent.com:sub`, then GitHub Actions from organizations or repositories outside of your control are able to assume roles associated with the GitHub IAM IdP in your AWS account\.

**Related terms**
+ [Configuring a role for GitHub OIDC identity provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_oidc.html#idp_oidc_Create_GitHub)

## General Warning – Policy size exceeds role trust policy quota<a name="access-analyzer-reference-policy-checks-general-warning-policy-size-exceeds-role-trust-policy-quota"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Policy size exceeds role trust policy quota: The characters in the role trust policy, excluding whitespace, exceed the character maximum. We recommend that you request a role trust policy length quota increase using Service Quotas and AWS Support Center. If the quotas have already been increased, then you can ignore this warning.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The characters in the role trust policy, excluding whitespace, exceed the character maximum. We recommend that you request a role trust policy length quota increase using Service Quotas and AWS Support Center. If the quotas have already been increased, then you can ignore this warning."
```

**Resolving the general warning**

IAM and AWS STS have quotas that limit the size of role trust policies\. The characters in the role trust policy, excluding whitespace, exceed the character maximum\. We recommend that you request a role trust policy length quota increase using Service Quotas and the AWS Support Center Console\.

**Related terms**
+ [IAM and AWS STS quotas, name requirements, and character limits](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_iam-quotas.html)

## Security Warning – Allow with NotPrincipal<a name="access-analyzer-reference-policy-checks-security-warning-allow-with-not-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Allow with NotPrincipal: Using Allow with NotPrincipal can be overly permissive. We recommend that you use Principal instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using Allow with NotPrincipal can be overly permissive. We recommend that you use Principal instead."
```

**Resolving the security warning**

Using `"Effect": "Allow"` with the `NotPrincipal` can be overly permissive\. For example, this can grant permissions to anonymous principals\. AWS recommends that you specify principals that need access using the `Principal` element\. Alternatively, you can allow broad access and then add another statement that uses the `NotPrincipal` element with `“Effect”: “Deny”`\.
+ [AWS JSON policy elements: Principal](reference_policies_elements_principal.md)
+ [AWS JSON policy elements: NotPrincipal](reference_policies_elements_notprincipal.md)

## Security Warning – ForAllValues with single valued key<a name="access-analyzer-reference-policy-checks-security-warning-forallvalues-with-single-valued-key"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
ForAllValues with single valued key: Using ForAllValues qualifier with the single-valued condition key {{key}} can be overly permissive. We recommend that you remove ForAllValues:.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using ForAllValues qualifier with the single-valued condition key {{key}} can be overly permissive. We recommend that you remove ForAllValues:."
```

**Resolving the security warning**

AWS recommends that you use the `ForAllValues` only with multivalued conditions\. The `ForAllValues` set operator tests whether the value of every member of the request set is a subset of the condition key set\. The condition returns true if every key value in the request matches at least one value in the policy\. It also returns true if there are no keys in the request, or if the key values resolve to a null data set, such as an empty string\.

To learn whether a condition supports a single value or multiple values, review the [Actions, resources, and condition keys](https://docs.aws.amazon.com/service-authorization/latest/reference/reference_policies_actions-resources-contextkeys.html) page for the service\. Condition keys with the `ArrayOf` data type prefix are multivalued condition keys\. For example, Amazon SES supports keys with single values \(`String`\) and the `ArrayOfString` multivalued data type\.
+ [Using multiple keys and values](reference_policies_multi-value-conditions.md#reference_policies_multi-key-or-value-conditions)

## Security Warning – Pass role with NotResource<a name="access-analyzer-reference-policy-checks-security-warning-pass-role-with-not-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Pass role with NotResource: Using the iam:PassRole action with NotResource can be overly permissive because it can allow iam:PassRole permissions on multiple resources. We recommend that you specify resource ARNs instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using the iam:PassRole action with NotResource can be overly permissive because it can allow iam:PassRole permissions on multiple resources. We recommend that you specify resource ARNs instead."
```

**Resolving the security warning**

To configure many AWS services, you must pass an IAM role to the service\. To allow this you must grant the `iam:PassRole` permission to an identity \(user, group of users, or role\)\. Using `iam:PassRole` in a policy with the `NotResource` element can allow your principals to access more services or features than you intended\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\. Additionally, you can reduce permissions to a single service by using the `iam:PassedToService` condition key\.
+ [Passing a role to a service](id_roles_use_passrole.md)
+ [iam:PassedToService](reference_policies_iam-condition-keys.md#ck_PassedToService)
+ [IAM JSON policy elements: NotResource](reference_policies_elements_notresource.md)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## Security Warning – Pass role with star in action and NotResource<a name="access-analyzer-reference-policy-checks-security-warning-pass-role-with-star-in-action-and-not-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Pass role with star in action and NotResource: Using an action with a wildcard (*) and NotResource can be overly permissive because it can allow iam:PassRole permissions on multiple resources. We recommend that you specify resource ARNs instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using an action with a wildcard (*) and NotResource can be overly permissive because it can allow iam:PassRole permissions on multiple resources. We recommend that you specify resource ARNs instead."
```

**Resolving the security warning**

To configure many AWS services, you must pass an IAM role to the service\. To allow this you must grant the `iam:PassRole` permission to an identity \(user, group of users, or role\)\. Policies with a wildcard \(\*\) in the `Action` and that include the `NotResource` element can allow your principals to access more services or features than you intended\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\. Additionally, you can reduce permissions to a single service by using the `iam:PassedToService` condition key\.
+ [Passing a role to a service](id_roles_use_passrole.md)
+ [iam:PassedToService](reference_policies_iam-condition-keys.md#ck_PassedToService)
+ [IAM JSON policy elements: NotResource](reference_policies_elements_notresource.md)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## Security Warning – Pass role with NotAction and NotResource<a name="access-analyzer-reference-policy-checks-security-warning-pass-role-with-not-action-and-not-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Pass role with NotAction and NotResource: Using NotAction with NotResource can be overly permissive because it can allow iam:PassRole permissions on multiple resources.. We recommend that you specify resource ARNs instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using NotAction with NotResource can be overly permissive because it can allow iam:PassRole permissions on multiple resources.. We recommend that you specify resource ARNs instead."
```

**Resolving the security warning**

To configure many AWS services, you must pass an IAM role to the service\. To allow this you must grant the `iam:PassRole` permission to an identity \(user, group of users, or role\)\. Using the `NotAction` element and listing some resources in the `NotResource` element can allow your principals to access more services or features than you intended\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\. Additionally, you can reduce permissions to a single service by using the `iam:PassedToService` condition key\.
+ [Passing a role to a service](id_roles_use_passrole.md)
+ [iam:PassedToService](reference_policies_iam-condition-keys.md#ck_PassedToService)
+ [IAM JSON policy elements: NotAction](reference_policies_elements_notaction.md)
+ [IAM JSON policy elements: Action](reference_policies_elements_action.md)
+ [IAM JSON policy elements: NotResource](reference_policies_elements_notresource.md)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## Security Warning – Pass role with star in resource<a name="access-analyzer-reference-policy-checks-security-warning-pass-role-with-star-in-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Pass role with star in resource: Using the iam:PassRole action with wildcards (*) in the resource can be overly permissive because it allows iam:PassRole permissions on multiple resources. We recommend that you specify resource ARNs or add the iam:PassedToService condition key to your statement.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using the iam:PassRole action with wildcards (*) in the resource can be overly permissive because it allows iam:PassRole permissions on multiple resources. We recommend that you specify resource ARNs or add the iam:PassedToService condition key to your statement."
```

**Resolving the security warning**

To configure many AWS services, you must pass an IAM role to the service\. To allow this you must grant the `iam:PassRole` permission to an identity \(user, group of users, or role\)\. Policies that allow `iam:PassRole` and that include a wildcard \(\*\) in the `Resource` element can allow your principals to access more services or features than you intended\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\. Additionally, you can reduce permissions to a single service by using the `iam:PassedToService` condition key\.

Some AWS services include their service namespace in the name of their role\. This policy check takes these conventions into account while analyzing the policy to generate findings\. For example, the following resource ARN might not generate a finding:

```
arn:aws:iam::*:role/Service*
```
+ [Passing a role to a service](id_roles_use_passrole.md)
+ [iam:PassedToService](reference_policies_iam-condition-keys.md#ck_PassedToService)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

### AWS managed policies with this security warning<a name="accan-ref-policy-check-message-fix-security-warning-pass-role-with-star-in-resource-awsmanpol"></a>

[AWS managed policies](access_policies_managed-vs-inline.md#aws-managed-policies) enable you to get started with AWS by assigning permissions based on general AWS use cases\.

One of those use cases is for administrators within your account\. The following AWS managed policies provide administrator access and grant permissions to pass any IAM role to any service\. AWS recommends that you attach the following AWS managed policies only to IAM identities that you consider administrators\.
+ [AdministratorAccess\-Amplify](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/AdministratorAccess-Amplify)

The following AWS managed policies include permissions to `iam:PassRole` with a wildcard \(\*\) in the resource and are on a [deprecation path](access_policies_managed-deprecated.md)\. For each of these policies, we updated the permission guidance, such as recommending a new AWS managed policy that supports the use case\. To view alternatives to these policies, see the guides for [each service](reference_aws-services-that-work-with-iam.md)\.
+ AWSElasticBeanstalkFullAccess
+ AWSElasticBeanstalkService
+ AWSLambdaFullAccess
+ AWSLambdaReadOnlyAccess
+ AWSOpsWorksFullAccess
+ AWSOpsWorksRole
+ AWSDataPipelineRole
+ AmazonDynamoDBFullAccesswithDataPipeline
+ AmazonElasticMapReduceFullAccess
+ AmazonDynamoDBFullAccesswithDataPipeline
+ AmazonEC2ContainerServiceFullAccess

The following AWS managed policies provide permissions for only [service\-linked roles](using-service-linked-roles.md), which allow AWS services to perform actions on your behalf\. You cannot attach these policies to your IAM identities\.
+ [AWSServiceRoleForAmazonEKSNodegroup](https://console.aws.amazon.com/iam/home#/policies/arn:aws:iam::aws:policy/aws-service-role/AWSServiceRoleForAmazonEKSNodegroup)

## Security Warning – Pass role with star in action and resource<a name="access-analyzer-reference-policy-checks-security-warning-pass-role-with-star-in-action-and-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Pass role with star in action and resource: Using wildcards (*) in the action and the resource can be overly permissive because it allows iam:PassRole permissions on all resources. We recommend that you specify resource ARNs or add the iam:PassedToService condition key to your statement.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using wildcards (*) in the action and the resource can be overly permissive because it allows iam:PassRole permissions on all resources. We recommend that you specify resource ARNs or add the iam:PassedToService condition key to your statement."
```

**Resolving the security warning**

To configure many AWS services, you must pass an IAM role to the service\. To allow this you must grant the `iam:PassRole` permission to an identity \(user, group of users, or role\)\. Policies with a wildcard \(\*\) in the `Action` and `Resource` elements can allow your principals to access more services or features than you intended\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\. Additionally, you can reduce permissions to a single service by using the `iam:PassedToService` condition key\.
+ [Passing a role to a service](id_roles_use_passrole.md)
+ [iam:PassedToService](reference_policies_iam-condition-keys.md#ck_PassedToService)
+ [IAM JSON policy elements: Action](reference_policies_elements_action.md)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

### AWS managed policies with this security warning<a name="accan-ref-policy-check-message-fix-security-warning-pass-role-with-star-in-action-and-resource-awsmanpol"></a>

[AWS managed policies](access_policies_managed-vs-inline.md#aws-managed-policies) enable you to get started with AWS by assigning permissions based on general AWS use cases\.

Some of those use cases are for administrators within your account\. The following AWS managed policies provide administrator access and grant permissions to pass any IAM role to any AWS service\. AWS recommends that you attach the following AWS managed policies to only the IAM identities that you consider administrators\.
+ [AdministratorAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/AdministratorAccess)
+ [IAMFullAccess](https://console.aws.amazon.com/iam/home#policies/arn:aws:iam::aws:policy/IAMFullAccess)

## Security Warning – Pass role with star in resource and NotAction<a name="access-analyzer-reference-policy-checks-security-warning-pass-role-with-star-in-resource-and-not-action"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Pass role with star in resource and NotAction: Using a resource with wildcards (*) and NotAction can be overly permissive because it allows iam:PassRole permissions on all resources. We recommend that you specify resource ARNs or add the iam:PassedToService condition key to your statement.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using a resource with wildcards (*) and NotAction can be overly permissive because it allows iam:PassRole permissions on all resources. We recommend that you specify resource ARNs or add the iam:PassedToService condition key to your statement."
```

**Resolving the security warning**

To configure many AWS services, you must pass an IAM role to the service\. To allow this you must grant the `iam:PassRole` permission to an identity \(user, group of users, or role\)\. Using the `NotAction` element in a policy with a wildcard \(\*\) in the `Resource` element can allow your principals to access more services or features than you intended\. AWS recommends that you specify allowed ARNs in the `Resource` element instead\. Additionally, you can reduce permissions to a single service by using the `iam:PassedToService` condition key\.
+ [Passing a role to a service](id_roles_use_passrole.md)
+ [iam:PassedToService](reference_policies_iam-condition-keys.md#ck_PassedToService)
+ [IAM JSON policy elements: NotAction](reference_policies_elements_notaction.md)
+ [IAM JSON policy elements: Action](reference_policies_elements_action.md)
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## Security Warning – Missing paired condition keys<a name="access-analyzer-reference-policy-checks-security-warning-missing-paired-condition-keys"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing paired condition keys: Using the condition key {{conditionKeyName}} can be overly permissive without also using the following condition keys: {{recommendedKeys}}. Condition keys like this one are more secure when paired with a related key. We recommend that you add the related condition keys to the same condition block.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using the condition key {{conditionKeyName}} can be overly permissive without also using the following condition keys: {{recommendedKeys}}. Condition keys like this one are more secure when paired with a related key. We recommend that you add the related condition keys to the same condition block."
```

**Resolving the security warning**

Some condition keys are more secure when paired with other related condition keys\. AWS recommends that you include the related condition keys in the same condition block as the existing condition key\. This makes the permissions granted through the policy more secure\.

For example, you can use the `aws:VpcSourceIp` condition key to compare the IP address from which a request was made with the IP address that you specify in the policy\. AWS recommends that you add the related `aws:SourceVPC` condition key\. This checks whether the request comes from the VPC that you specify in the policy *and* the IP address that you specify\.

**Related terms**
+ [`aws:VpcSourceIp` global condition key](reference_policies_condition-keys.md#condition-keys-vpcsourceip)
+ [`aws:SourceVPC` global condition key](reference_policies_condition-keys.md#condition-keys-sourcevpc)
+ [Global condition keys](reference_policies_condition-keys.md)
+ [Condition element](reference_policies_elements_condition.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Security Warning – Deny with unsupported tag condition key for service<a name="access-analyzer-reference-policy-checks-security-warning-deny-with-unsupported-tag-condition-key-for-service"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Deny with unsupported tag condition key for service: Using the effect Deny with the tag condition key {{conditionKeyName}} and actions for services with the following prefixes can be overly permissive: {{serviceNames}}. Actions for the listed services are not denied by this statement. We recommend that you move these actions to a different statement without this condition key.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using the effect Deny with the tag condition key {{conditionKeyName}} and actions for services with the following prefixes can be overly permissive: {{serviceNames}}. Actions for the listed services are not denied by this statement. We recommend that you move these actions to a different statement without this condition key."
```

**Resolving the security warning**

Using unsupported tag condition keys in the `Condition` element of a policy with `"Effect": "Deny"` can be overly permissive, because the condition is ignored for that service\. AWS recommends that you remove the service actions that don’t support the condition key and create another statement to deny access to specific resources for those actions\.

If you use the `aws:ResourceTag` condition key and it’s not supported by a service action, then the key is not included in the request context\. In this case, the condition in the `Deny` statement always returns `false` and the action is never denied\. This happens even if the resource is tagged correctly\.

When a service supports the `aws:ResourceTag` condition key, you can use tags to control access to that service’s resources\. This is known as [attribute\-based access control \(ABAC\)](introduction_attribute-based-access-control.md)\. Services that don’t support these keys require you to control access to resources using [resource\-based access control \(RBAC\)](introduction_attribute-based-access-control.md#introduction_attribute-based-access-control_compare-rbac)\.

**Note**  
Some services allow support for the `aws:ResourceTag` condition key for a subset of their resources and actions\. IAM Access Analyzer returns findings for the service actions that are not supported\. For example, Amazon S3 supports `aws:ResourceTag` for a subset of its resources\. To view all of the resource types available in Amazon S3 that support the `aws:ResourceTag` condition key, see [Resource types defined by Amazon S3](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazons3.html#amazons3-resources-for-iam-policies) in the Service Authorization Reference\.

For example, assume that you want to deny access to untag delete specific resources that are tagged with the key\-value pair `status=Confidential`\. Also assume that AWS Lambda allows you to tag and untag resources, but doesn’t support the `aws:ResourceTag` condition key\. To deny the delete actions for AWS App Mesh and AWS Backup if this tag is present, use the `aws:ResourceTag` condition key\. For Lambda, use a resource naming convention that includes the `"Confidential"` prefix\. Then include a separate statement that prevents deleting resources with that naming convention\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "DenyDeleteSupported",
            "Effect": "Deny",
            "Action": [
                "appmesh:DeleteMesh", 
                "backup:DeleteBackupPlan"
                ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:ResourceTag/status": "Confidential"
                }
            }
        },
        {
            "Sid": "DenyDeleteUnsupported",
            "Effect": "Deny",
            "Action": "lambda:DeleteFunction",
            "Resource": "arn:aws:lambda:*:123456789012:function:status-Confidential*"
        }
    ]
}
```

**Warning**  
Do not use the …[IfExists](reference_policies_elements_condition_operators.md#Conditions_IfExists) version of the condition operator as a workaround for this finding\. This means "Deny the action if the key is present in the request context and the values match\. Otherwise, deny the action\." In the previous example, including the `lambda:DeleteFunction` action in the `DenyDeleteSupported` statement with the `StringEqualsIfExists` operator always denies the action\. For that action, the key is not present in the context, and every attempt to delete that resource type is denied, regardless of whether the resource is tagged\.

**Related terms**
+ [Global condition keys](reference_policies_condition-keys.md)
+ [Comparing ABAC to RBAC](introduction_attribute-based-access-control.md#introduction_attribute-based-access-control_compare-rbac)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)
+ [Condition element](reference_policies_elements_condition.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Security Warning – Deny NotAction with unsupported tag condition key for service<a name="access-analyzer-reference-policy-checks-security-warning-deny-notaction-with-unsupported-tag-condition-key-for-service"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Deny NotAction with unsupported tag condition key for service: Using the effect Deny with NotAction and the tag condition key {{conditionKeyName}} can be overly permissive because some service actions are not denied by this statement. This is because the condition key doesn't apply to some service actions. We recommend that you use Action instead of NotAction.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using the effect Deny with NotAction and the tag condition key {{conditionKeyName}} can be overly permissive because some service actions are not denied by this statement. This is because the condition key doesn't apply to some service actions. We recommend that you use Action instead of NotAction."
```

**Resolving the security warning**

Using tag condition keys in the `Condition` element of a policy with the element `NotAction` and `"Effect": "Deny"` can be overly permissive\. The condition is ignored for service actions that don’t support the condition key\. AWS recommends that you rewrite the logic to deny a list of actions\.

If you use the `aws:ResourceTag` condition key with `NotAction`, any new or existing service actions that don’t support the key are not denied\. AWS recommends that you explicitly list the actions that you want to deny\. IAM Access Analyzer returns a separate finding for listed actions that don’t support the `aws:ResourceTag` condition key\. For more information, see [Security Warning – Deny with unsupported tag condition key for service](#access-analyzer-reference-policy-checks-security-warning-deny-with-unsupported-tag-condition-key-for-service)\. 

When a service supports the `aws:ResourceTag` condition key, you can use tags to control access to that service’s resources\. This is known as [attribute\-based access control \(ABAC\)](introduction_attribute-based-access-control.md)\. Services that don’t support these keys require you to control access to resources using [resource\-based access control \(RBAC\)](introduction_attribute-based-access-control.md#introduction_attribute-based-access-control_compare-rbac)\.

**Related terms**
+ [Global condition keys](reference_policies_condition-keys.md)
+ [Comparing ABAC to RBAC](introduction_attribute-based-access-control.md#introduction_attribute-based-access-control_compare-rbac)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)
+ [Condition element](reference_policies_elements_condition.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Security Warning – Restrict access to service principal<a name="access-analyzer-reference-policy-checks-security-warning-restrict-access-to-service-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Restrict access to service principal: Granting access to a service principal without specifying a source is overly permissive. Use aws:SourceArn or aws:SourceAccount condition key and scope access to a specific source to grant fine-grained access.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Granting access to a service principal without specifying a source is overly permissive. Use aws:SourceArn or aws:SourceAccount condition key and scope access to a specific source to grant fine-grained access."
```

**Resolving the security warning**

You can specify AWS services in the `Principal` element of a resource\-based policy using a *service principal*, which is an identifier for the service\. When granting access to a service principal to act on your behalf, restrict access\. You can prevent overly permissive policies by using the `aws:SourceAccount` or `aws:SourceArn` condition keys to restrict access to a specific source, such as a specific resource ARN or AWS account\. Restricting access helps you prevent a security issue called the *confused deputy problem*\.

**Related terms**
+ [Service principals](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-services)
+ [AWS global condition keys: aws:SourceAccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount)
+ [AWS global condition keys: aws:SourceArn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn)
+ [The confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html#cross-service-confused-deputy-prevention)

## Security Warning – Missing condition key for oidc principal<a name="access-analyzer-reference-policy-checks-security-warning-missing-condition-key-for-oidc-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing condition key for oidc principal: Using an Open ID Connect principal without a condition can be overly permissive. Add condition keys with a prefix that matches your federated OIDC principals to ensure that only the intended identity provider assumes the role.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using an Open ID Connect principal without a condition can be overly permissive. Add condition keys with a prefix that matches your federated OIDC principals to ensure that only the intended identity provider assumes the role."
```

**Resolving the security warning**

Using an Open ID Connect principal without a condition can be overly permissive\. Add condition keys with a prefix that matches your federated OIDC principals to ensure that only the intended identity provider assumes the role\.

**Related terms**
+ [Creating a role for web identity or OpenID Connect Federation \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_oidc.html)

## Security Warning – Missing github repo condition key<a name="access-analyzer-reference-policy-checks-security-warning-missing-github-repo-condition-key"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Missing github repo condition key: Granting a federated GitHub principal permissions without a condition key can allow more sources to assume the role than you intended. Add the token.actions.githubusercontent.com:sub condition key and specify the branch and repository name in the value.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Granting a federated GitHub principal permissions without a condition key can allow more sources to assume the role than you intended. Add the token.actions.githubusercontent.com:sub condition key and specify the branch and repository name in the value."
```

**Resolving the security warning**

If you use GitHub as an OIDC IdP, best practice is to limit the entities that can assume the role associated with the IAM IdP\. When you include a `Condition` statement in a role trust policy, you can limit the role to a specific GitHub organization, repository, or branch\. You can use the condition key `token.actions.githubusercontent.com:sub` to limit access\. We recommend that you limit the condition to a specific set of repositories or branches\. If you do not include this condition, then GitHub Actions from organizations or repositories outside of your control are able to assume roles associated with the GitHub IAM IdP in your AWS account\.

**Related terms**
+ [Configuring a role for GitHub OIDC identity provider](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_oidc.html#idp_oidc_Create_GitHub)

## Suggestion – Empty array action<a name="access-analyzer-reference-policy-checks-suggestion-empty-array-action"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty array action: This statement includes no actions and does not affect the policy. Specify actions.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "This statement includes no actions and does not affect the policy. Specify actions."
```

**Resolving the suggestion**

Statements must include either an `Action` or `NotAction` element that includes a set of actions\. When the element is empty, the policy statement provides no permissions\. Specify actions in the `Action` element\.
+ [IAM JSON policy elements: Action](reference_policies_elements_action.md)

## Suggestion – Empty array condition<a name="access-analyzer-reference-policy-checks-suggestion-empty-array-condition"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty array condition: There are no values for the condition key {{key}} and it does not affect the policy. Specify conditions.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "There are no values for the condition key {{key}} and it does not affect the policy. Specify conditions."
```

**Resolving the suggestion**

The optional `Condition` element structure requires that you use a condition operator and a key\-value pair\. When the condition value is empty, the condition returns `true` and the policy statement provides no permissions\. Specify a condition value\.
+ [IAM JSON policy elements: Condition ](reference_policies_elements_condition.md)

## Suggestion – Empty array condition ForAllValues<a name="access-analyzer-reference-policy-checks-suggestion-empty-array-condition-forallvalues"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty array condition ForAllValues: The ForAllValues prefix with an empty condition key matches only if the key {{key}} is missing from the request context. To determine if the request context is empty, we recommend that you use the Null condition operator with the value of true instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The ForAllValues prefix with an empty condition key matches only if the key {{key}} is missing from the request context. To determine if the request context is empty, we recommend that you use the Null condition operator with the value of true instead."
```

**Resolving the suggestion**

The `Condition` element structure requires that you use a condition operator and a key\-value pair\. The `ForAllValues` set operator tests whether the value of every member of the request set is a subset of the condition key set\. 

When you use `ForAllValues` with an empty condition key, the condition matches only if there are no keys in the request\. AWS recommends that if you want to test whether a request context is empty, use the `Null` condition operator instead\.
+ [Using multiple keys and values](reference_policies_multi-value-conditions.md#reference_policies_multi-key-or-value-conditions)
+ [Null condition operator](reference_policies_elements_condition_operators.md#Conditions_Null)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Suggestion – Empty array condition ForAnyValue<a name="access-analyzer-reference-policy-checks-suggestion-empty-array-condition-foranyvalue"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty array condition ForAnyValue: The ForAnyValue prefix with an empty condition key {{key}} never matches the request context and it does not affect the policy. Specify conditions.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The ForAnyValue prefix with an empty condition key {{key}} never matches the request context and it does not affect the policy. Specify conditions."
```

**Resolving the suggestion**

The `Condition` element structure requires that you use a condition operator and a key\-value pair\. The `ForAnyValues` set operator tests whether at least one member of the set of request values matches at least one member of the set of condition key values\.

When you use `ForAnyValues` with an empty condition key, the condition never matches\. This means that the statement has no effect on the policy\. AWS recommends that you rewrite the condition\.
+ [Using multiple keys and values](reference_policies_multi-value-conditions.md#reference_policies_multi-key-or-value-conditions)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Suggestion – Empty array condition IfExists<a name="access-analyzer-reference-policy-checks-suggestion-empty-array-condition-ifexists"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty array condition IfExists: The IfExists suffix with an empty condition key matches only if the key {{key}} is missing from the request context. To determine if the request context is empty, we recommend that you use the Null condition operator with the value of true instead.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The IfExists suffix with an empty condition key matches only if the key {{key}} is missing from the request context. To determine if the request context is empty, we recommend that you use the Null condition operator with the value of true instead."
```

**Resolving the suggestion**

The `...IfExists` suffix edits a condition operator\. It means that if the policy key is present in the context of the request, process the key as specified in the policy\. If the key is not present, evaluate the condition element as true\.

When you use `...IfExists` with an empty condition key, the condition matches only if there are no keys in the request\. AWS recommends that if you want to test whether a request context is empty, use the `Null` condition operator instead\.
+ [\.\.\.IfExists condition operators](reference_policies_elements_condition_operators.md#Conditions_IfExists)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Suggestion – Empty array principal<a name="access-analyzer-reference-policy-checks-suggestion-empty-array-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty array principal: This statement includes no principals and does not affect the policy. Specify principals.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "This statement includes no principals and does not affect the policy. Specify principals."
```

**Resolving the suggestion**

You must use the `Principal` or `NotPrincipal` element in the trust policies for IAM roles and in resource\-based policies\. Resource\-based policies are policies that you embed directly in a resource\.

When you provide an empty array in a statement's `Principal` element, the statement has no effect on the policy\. AWS recommends that you specify the principals that should have access to the resource\.
+ [IAM JSON policy elements: Principal](reference_policies_elements_principal.md)
+ [IAM JSON policy elements: NotPrincipal](reference_policies_elements_notprincipal.md)

## Suggestion – Empty array resource<a name="access-analyzer-reference-policy-checks-suggestion-empty-array-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty array resource: This statement includes no resources and does not affect the policy. Specify resources.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "This statement includes no resources and does not affect the policy. Specify resources."
```

**Resolving the suggestion**

Statements must include either a `Resource` or a `NotResource` element\.

When you provide an empty array in a statement's resource element, the statement has no effect on the policy\. AWS recommends that you specify Amazon Resource Names \(ARNs\) for resources\.
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)
+ [IAM JSON policy elements: NotResource](reference_policies_elements_notresource.md)

## Suggestion – Empty object condition<a name="access-analyzer-reference-policy-checks-suggestion-empty-object-condition"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty object condition: This condition block is empty and it does not affect the policy. Specify conditions.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "This condition block is empty and it does not affect the policy. Specify conditions."
```

**Resolving the suggestion**

The `Condition` element structure requires that you use a condition operator and a key\-value pair\.

When you provide an empty object in a statement's condition element, the statement has no effect on the policy\. Remove the optional element or specify conditions\.
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Suggestion – Empty object principal<a name="access-analyzer-reference-policy-checks-suggestion-empty-object-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty object principal: This statement includes no principals and does not affect the policy. Specify principals.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "This statement includes no principals and does not affect the policy. Specify principals."
```

**Resolving the suggestion**

You must use the `Principal` or `NotPrincipal` element in the trust policies for IAM roles and in resource\-based policies\. Resource\-based policies are policies that you embed directly in a resource\.

When you provide an empty object in a statement's `Principal` element, the statement has no effect on the policy\. AWS recommends that you specify the principals that should have access to the resource\.
+ [IAM JSON policy elements: Principal](reference_policies_elements_principal.md)
+ [IAM JSON policy elements: NotPrincipal](reference_policies_elements_notprincipal.md)

## Suggestion – Empty Sid value<a name="access-analyzer-reference-policy-checks-suggestion-empty-sid-value"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Empty Sid value: Add a value to the empty string in the Sid element.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Add a value to the empty string in the Sid element."
```

**Resolving the suggestion**

The optional `Sid` \(statement ID\) element allows you to enter an identifier that you provide for the policy statement\. You can assign an `Sid` value to each statement in a statement array\. If you choose to use the `Sid` element, you must provide a string value\.

**Related terms**
+ [IAM JSON policy elements: Sid](reference_policies_elements_sid.md)

## Suggestion – Improve IP range<a name="access-analyzer-reference-policy-checks-suggestion-improve-ip-range"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Improve IP range: The non-zero bits in the IP address after the masked bits are ignored. Replace address with {{addr}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The non-zero bits in the IP address after the masked bits are ignored. Replace address with {{addr}}."
```

**Resolving the suggestion**

IP address conditions must be in the standard CIDR format, such as 203\.0\.113\.0/24 or 2001:DB8:1234:5678::/64\. When you include non\-zero bits after the masked bits, they are not considered for the condition\. AWS recommends that you use the new address included in the message\.
+ [IP address condition operators](reference_policies_elements_condition_operators.md#Conditions_IPAddress)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Suggestion – Null with qualifier<a name="access-analyzer-reference-policy-checks-suggestion-null-with-qualifier"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Null with qualifier: Avoid using the Null condition operator with the ForAllValues or ForAnyValue qualifiers because they always return a true or false respectively.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Avoid using the Null condition operator with the ForAllValues or ForAnyValue qualifiers because they always return a true or false respectively."
```

**Resolving the suggestion**

In the `Condition` element, you build expressions in which you use condition operators like equal or less than to compare a condition in the policy against keys and values in the request context\. For requests that include multiple values for a single condition key, you must use the  `ForAllValues` or `ForAnyValue` set operators\.

When you use the `Null` condition operator with `ForAllValues`, the statement always returns `true`\. When you use the `Null` condition operator with `ForAnyValue`, the statement always returns `false`\. AWS recommends that you use the `StringLike` condition operator with these set operators\.

**Related terms**
+ [Using multiple condition keys and values](reference_policies_multi-value-conditions.md#reference_policies_multi-key-or-value-conditions)
+ [Null condition operator](reference_policies_elements_condition_operators.md#Conditions_Null)
+ [Condition element](reference_policies_elements_condition.md)

## Suggestion – Private IP address subset<a name="access-analyzer-reference-policy-checks-suggestion-private-ip-address-subset"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Private IP address subset: The values for condition key aws:SourceIp include a mix of private and public IP addresses. The private addresses will not have the desired effect. aws:SourceIp works only for public IP address ranges. To define permissions for private IP ranges, use aws:VpcSourceIp.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The values for condition key aws:SourceIp include a mix of private and public IP addresses. The private addresses will not have the desired effect. aws:SourceIp works only for public IP address ranges. To define permissions for private IP ranges, use aws:VpcSourceIp."
```

**Resolving the suggestion**

The global condition key `aws:SourceIp` works only for public IP address ranges\.

When your `Condition` element includes a mix of private and public IP addresses, the statement might not have the desired effect\. You can specify private IP addresses using `aws:VpcSourceIP`\.

**Note**  
The global condition key `aws:VpcSourceIP` matches only if the request originates from the specified IP address and it goes through a VPC endpoint\.
+ [aws:SourceIp global condition key](reference_policies_condition-keys.md#condition-keys-sourceip)
+ [aws:VpcSourceIp global condition key](reference_policies_condition-keys.md#condition-keys-vpcsourceip)
+ [IP address condition operators](reference_policies_elements_condition_operators.md#Conditions_IPAddress)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Suggestion – Private NotIpAddress subset<a name="access-analyzer-reference-policy-checks-suggestion-private-not-ip-address-subset"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Private NotIpAddress subset: The values for condition key aws:SourceIp include a mix of private and public IP addresses. The private addresses have no effect. aws:SourceIp works only for public IP address ranges. To define permissions for private IP ranges, use aws:VpcSourceIp.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The values for condition key aws:SourceIp include a mix of private and public IP addresses. The private addresses have no effect. aws:SourceIp works only for public IP address ranges. To define permissions for private IP ranges, use aws:VpcSourceIp."
```

**Resolving the suggestion**

The global condition key `aws:SourceIp` works only for public IP address ranges\.

When your `Condition` element includes the `NotIpAddress` condition operator and a mix of private and public IP addresses, the statement might not have the desired effect\. Every public IP addresses that is not specified in the policy will match\. No private IP addresses will match\. To achieve this effect, you can use `NotIpAddress` with `aws:VpcSourceIP` and specify the private IP addresses that should not match\.
+ [aws:SourceIp global condition key](reference_policies_condition-keys.md#condition-keys-sourceip)
+ [aws:VpcSourceIp global condition key](reference_policies_condition-keys.md#condition-keys-vpcsourceip)
+ [IP address condition operators](reference_policies_elements_condition_operators.md#Conditions_IPAddress)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Suggestion – Redundant action<a name="access-analyzer-reference-policy-checks-suggestion-redundant-action"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Redundant action: The {{redundantActionCount}} action(s) are redundant because they provide similar permissions. Update the policy to remove the redundant action such as: {{redundantAction}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The {{redundantActionCount}} action(s) are redundant because they provide similar permissions. Update the policy to remove the redundant action such as: {{redundantAction}}."
```

**Resolving the suggestion**

When you use wildcards \(\*\) in the `Action` element, you can include redundant permissions\. AWS recommends that you review your policy and include only the permissions that you need\. This can help you remove redundant actions\.

For example, the following actions include the `iam:GetCredentialReport` action twice\.

```
"Action": [
        "iam:Get*",
        "iam:List*",
        "iam:GetCredentialReport"
    ],
```

In this example, permissions are defined for every IAM action that begins with `Get` or `List`\. When IAM adds additional get or list operations, this policy will allow them\. You might want to allow all of these read\-only actions\. The `iam:GetCredentialReport` action is already included as part of `iam:Get*`\. To remove the duplicate permissions, you could remove `iam:GetCredentialReport`\.

You receive a finding for this policy check when all of the contents of an action are redundant\. In this example, if the element included `iam:*CredentialReport`, it is not considered redundant\. That includes `iam:GetCredentialReport`, which is redundant, and `iam:GenerateCredentialReport`, which is not\. Removing either `iam:Get*` or `iam:*CredentialReport` would change the policy's permissions\.
+ [IAM JSON policy elements: Action](reference_policies_elements_action.md)

### AWS managed policies with this suggestion<a name="accan-ref-policy-check-message-fix-suggestion-redundant-action-awsmanpol"></a>

[AWS managed policies](access_policies_managed-vs-inline.md#aws-managed-policies) enable you to get started with AWS by assigning permissions based on general AWS use cases\.

Redundant actions do not affect the permissions granted by the policy\. When using an AWS managed policy as a reference to create your customer managed policy, AWS recommends that you remove redundant actions from your policy\.

## Suggestion – Redundant condition value num<a name="access-analyzer-reference-policy-checks-suggestion-redundant-condition-value-num"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Redundant condition value num: Multiple values in {{operator}} are redundant. Replace with the {{greatest/least}} single value for {{key}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Multiple values in {{operator}} are redundant. Replace with the {{greatest/least}} single value for {{key}}."
```

**Resolving the suggestion**

When you use numeric condition operators for similar values in a condition key, you can create an overlap that results in redundant permissions\.

For example, the following `Condition` element includes multiple `aws:MultiFactorAuthAge` conditions that have an age overlap of 1200 seconds\.

```
"Condition": {
        "NumericLessThan": {
          "aws:MultiFactorAuthAge": [
            "2700",
            "3600"
          ]
        }
      }
```

In this example, the permissions are defined if multi\-factor authentication \(MFA\) was completed less than 3600 seconds \(1 hour\) ago\. You could remove the redundant `2700` value\.
+ [Numeric condition operators](reference_policies_elements_condition_operators.md#Conditions_Numeric)
+ [IAM JSON policy elements: Condition](reference_policies_elements_condition.md)

## Suggestion – Redundant resource<a name="access-analyzer-reference-policy-checks-suggestion-redundant-resource"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Redundant resource: The {{redundantResourceCount}} resource ARN(s) are redundant because they reference the same resource. Review the use of wildcards (*)
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The {{redundantResourceCount}} resource ARN(s) are redundant because they reference the same resource. Review the use of wildcards (*)"
```

**Resolving the suggestion**

When you use wildcards \(\*\) in Amazon Resource Names \(ARNs\), you can create redundant resource permissions\.

For example, the following `Resource` element includes multiple ARNs with redundant permissions\.

```
"Resource": [
            "arn:aws:iam::111122223333:role/jane-admin",
            "arn:aws:iam::111122223333:role/jane-s3only",
            "arn:aws:iam::111122223333:role/jane*"
        ],
```

In this example, the permissions are defined for any role with a name starting with `jane`\. You could remove the redundant `jane-admin` and `jane-s3only` ARNs without changing the resulting permissions\. This does make the policy dynamic\. It will define permissions for any future roles that begin with `jane`\. If the intention of the policy is to allow access to a static number of roles, then remove the last ARN and list only the ARNs that should be defined\.
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

### AWS managed policies with this suggestion<a name="accan-ref-policy-check-message-fix-suggestion-redundant-resource-awsmanpol"></a>

[AWS managed policies](access_policies_managed-vs-inline.md#aws-managed-policies) enable you to get started with AWS by assigning permissions based on general AWS use cases\.

Redundant resources do not affect the permissions granted by the policy\. When using an AWS managed policy as a reference to create your customer managed policy, AWS recommends that you remove redundant resources from your policy\.

## Suggestion – Redundant statement<a name="access-analyzer-reference-policy-checks-suggestion-redundant-statement"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Redundant statement: The statements are redundant because they provide identical permissions. Update the policy to remove the redundant statement.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The statements are redundant because they provide identical permissions. Update the policy to remove the redundant statement."
```

**Resolving the suggestion**

The `Statement` element is the main element for a policy\. This element is required\. The `Statement` element can contain a single statement or an array of individual statements\.

When you include the same statement more than once in a long policy, the statements are is redundant\. You can remove one of the statements without affecting the permissions granted by the policy\. When someone edits a policy, they might change one of the statements without updating the duplicate\. This might result in more permissions than intended\.
+ [IAM JSON policy elements: Statement](reference_policies_elements_statement.md)

## Suggestion – Wildcard in service name<a name="access-analyzer-reference-policy-checks-suggestion-wildcard-in-service-name"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Wildcard in service name: Avoid using wildcards (*, ?) in the service name because it might grant unintended access to other AWS services with similar names.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Avoid using wildcards (*, ?) in the service name because it might grant unintended access to other AWS services with similar names."
```

**Resolving the suggestion**

When you include the name of an AWS service in a policy, AWS recommends that you do not include wildcards \(\*, ?\)\. This might add permissions for future services that you do not intend\. For example, there are more than a dozen AWS services with the word `*code*` in their name\.

```
"Resource": "arn:aws:*code*::111122223333:*"
```
+ [IAM JSON policy elements: Resource](reference_policies_elements_resource.md)

## Suggestion – Allow with unsupported tag condition key for service<a name="access-analyzer-reference-policy-checks-suggestion-allow-with-unsupported-tag-condition-key-for-service"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Allow with unsupported tag condition key for service: Using the effect Allow with the tag condition key {{conditionKeyName}} and actions for services with the following prefixes does not affect the policy: {{serviceNames}}. Actions for the listed service are not allowed by this statement. We recommend that you move these actions to a different statement without this condition key.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using the effect Allow with the tag condition key {{conditionKeyName}} and actions for services with the following prefixes does not affect the policy: {{serviceNames}}. Actions for the listed service are not allowed by this statement. We recommend that you move these actions to a different statement without this condition key."
```

**Resolving the suggestion**

Using unsupported tag condition keys in the `Condition` element of a policy with `"Effect": "Allow"` does not affect the permissions granted by the policy, because the condition is ignored for that service action\. AWS recommends that you remove the actions for services that don’t support the condition key and create another statement to allow access to specific resources in that service\.

If you use the `aws:ResourceTag` condition key and it’s not supported by a service action, then the key is not included in the request context\. In this case, the condition in the `Allow` statement always returns `false` and the action is never allowed\. This happens even if the resource is tagged correctly\. 

When a service supports the `aws:ResourceTag` condition key, you can use tags to control access to that service’s resources\. This is known as [attribute\-based access control \(ABAC\)](introduction_attribute-based-access-control.md)\. Services that don’t support these keys require you to control access to resources using [resource\-based access control \(RBAC\)](introduction_attribute-based-access-control.md#introduction_attribute-based-access-control_compare-rbac)\.

**Note**  
Some services allow support for the `aws:ResourceTag` condition key for a subset of their resources and actions\. IAM Access Analyzer returns findings for the service actions that are not supported\. For example, Amazon S3 supports `aws:ResourceTag` for a subset of its resources\. To view all of the resource types available in Amazon S3 that support the `aws:ResourceTag` condition key, see [Resource types defined by Amazon S3](https://docs.aws.amazon.com/service-authorization/latest/reference/list_amazons3.html#amazons3-resources-for-iam-policies) in the Service Authorization Reference\.

For example, assume that you want to allow team members to view details for specific resources that are tagged with the key\-value pair `team=BumbleBee`\. Also assume that AWS Lambda allows you to tag resources, but doesn’t support the `aws:ResourceTag` condition key\. To allow view actions for AWS App Mesh and AWS Backup if this tag is present, use the `aws:ResourceTag` condition key\. For Lambda, use a resource naming convention that includes the team name as a prefix\. Then include a separate statement that allows viewing resources with that naming convention\.

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowViewSupported",
            "Effect": "Allow",
            "Action": [
                "appmesh:DescribeMesh", 
                "backup:GetBackupPlan"
                ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:ResourceTag/team": "BumbleBee"
                }
            }
        },
        {
            "Sid": "AllowViewUnsupported",
            "Effect": "Allow",
            "Action": "lambda:GetFunction",
            "Resource": "arn:aws:lambda:*:123456789012:function:team-BumbleBee*"
        }
    ]
}
```

**Warning**  
Do not use the `Not` [version of the condition operator](reference_policies_elements_condition_operators.md) with `"Effect": "Allow"` as a workaround for this finding\. These condition operators provide negated matching\. This means that after the condition is evaluated, the result is negated\. In the previous example, including the `lambda:GetFunction` action in the `AllowViewSupported` statement with the `StringNotEquals` operator always allows the action, regardless of whether the resource is tagged\.  
Do not use the …[IfExists](reference_policies_elements_condition_operators.md#Conditions_IfExists) version of the condition operator as a workaround for this finding\. This means "Allow the action if the key is present in the request context and the values match\. Otherwise, allow the action\." In the previous example, including the `lambda:GetFunction` action in the `AllowViewSupported` statement with the `StringEqualsIfExists` operator always allows the action\. For that action, the key is not present in the context, and every attempt to view that resource type is allowed, regardless of whether the resource is tagged\.

**Related terms**
+ [Global condition keys](reference_policies_condition-keys.md)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)
+ [Condition element](reference_policies_elements_condition.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Suggestion – Allow NotAction with unsupported tag condition key for service<a name="access-analyzer-reference-policy-checks-suggestion-allow-notaction-with-unsupported-tag-condition-key-for-service"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Allow NotAction with unsupported tag condition key for service: Using the effect Allow with NotAction and the tag condition key {{conditionKeyName}} allows only service actions that support the condition key. The condition key doesn't apply to some service actions. We recommend that you use Action instead of NotAction.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "Using the effect Allow with NotAction and the tag condition key {{conditionKeyName}} allows only service actions that support the condition key. The condition key doesn't apply to some service actions. We recommend that you use Action instead of NotAction."
```

**Resolving the suggestion**

Using unsupported tag condition keys in the `Condition` element of a policy with the element `NotAction` and `"Effect": "Allow"` does not affect the permissions granted by the policy\. The condition is ignored for service actions that don’t support the condition key\. AWS recommends that you rewrite the logic to allow a list of actions\.

If you use the `aws:ResourceTag` condition key with `NotAction`, any new or existing service actions that don’t support the key are not allowed\. AWS recommends that you explicitly list the actions that you want to allow\. IAM Access Analyzer returns a separate finding for listed actions that don’t support the `aws:ResourceTag` condition key\. For more information, see [Suggestion – Allow with unsupported tag condition key for service](#access-analyzer-reference-policy-checks-suggestion-allow-with-unsupported-tag-condition-key-for-service)\.

When a service supports the `aws:ResourceTag` condition key, you can use tags to control access to that service’s resources\. This is known as [attribute\-based access control \(ABAC\)](introduction_attribute-based-access-control.md)\. Services that don’t support these keys require you to control access to resources using [resource\-based access control \(RBAC\)](introduction_attribute-based-access-control.md#introduction_attribute-based-access-control_compare-rbac)\.

**Related terms**
+ [Global condition keys](reference_policies_condition-keys.md)
+ [Comparing ABAC to RBAC](introduction_attribute-based-access-control.md#introduction_attribute-based-access-control_compare-rbac)
+ [IAM JSON policy elements: Condition operators](reference_policies_elements_condition_operators.md)
+ [Condition element](reference_policies_elements_condition.md)
+ [Overview of JSON policies](access_policies.md#access_policies-json)

## Suggestion – Recommended condition key for service principal<a name="access-analyzer-reference-policy-checks-suggestion-recommended-condition-key-for-service-principal"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Recommended condition key for service principal: To restrict access to the service principal {{servicePrincipalPrefix}} operating on your behalf, we recommend aws:SourceArn or aws:SourceAccount instead of {{key}}.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "To restrict access to the service principal {{servicePrincipalPrefix}} operating on your behalf, we recommend aws:SourceArn or aws:SourceAccount instead of {{key}}."
```

**Resolving the suggestion**

You can specify AWS services in the `Principal` element of a resource\-based policy using a *service principal*, which is an identifier for the service\. You should use the `aws:SourceAccount` or `aws:SourceArn` condition keys when granting access to service principals instead of other condition keys, such as `aws:Referer`\. This helps you prevent a security issue called the *confused deputy problem*\.

**Related terms**
+ [Service principals](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-services)
+ [AWS global condition keys: aws:SourceAccount](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourceaccount)
+ [AWS global condition keys: aws:SourceArn](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-sourcearn)
+ [The confused deputy problem](https://docs.aws.amazon.com/IAM/latest/UserGuide/confused-deputy.html#cross-service-confused-deputy-prevention)

## Suggestion – Irrelevant condition key in policy<a name="access-analyzer-reference-policy-checks-suggestion-irrelevant-condition-key-in-policy"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Irrelevant condition key in policy: The condition key {{condition-key}} is not relevant for the {{resource-type}} policy.  Use this key in an identity-based policy to govern access to this resource.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The condition key {{condition-key}} is not relevant for the {{resource-type}} policy.  Use this key in an identity-based policy to govern access to this resource."
```

**Resolving the suggestion**

Some condition keys aren't relevant for resource\-based policies\. For example, the `s3:ResourceAccount` condition key isn't relevant for the resource\-based policy attached to an Amazon S3 bucket or Amazon S3 access point resource type\.

You should use the condition key in an identity\-based policy to control access to the resource\.

**Related terms**
+ [Identity\-based policies and resource\-based policies](access_policies_identity-vs-resource.md)

## Suggestion – Redundant principal in role trust policy<a name="access-analyzer-reference-policy-checks-suggestion-redundant-principal-in-role-trust-policy"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Redundant principal in role trust policy: The assumed-role principal {{redundant_principal}} is redundant with its parent role {{parent_role}}. Remove the assumed-role principal.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The assumed-role principal {{redundant_principal}} is redundant with its parent role {{parent_role}}. Remove the assumed-role principal."
```

**Resolving the suggestion**

If you specify both an assumed\-role principal and its parent role in the `Principal` element of a policy, it does not allow or deny any different permissions\. For example, it is redundant if you specify the `Principal` element using the following format:

```
"Principal": {
            "AWS": [
            "arn:aws:iam::AWS-account-ID:role/rolename",
            "arn:aws:iam::AWS-account-ID:assumed-role/rolename/rolesessionname"
        ]
```

We recommend removing the assumed\-role principal\.

**Related terms**
+ [Role session principals](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements_principal.html#principal-role-session)

## Suggestion – Confirm audience claim type<a name="access-analyzer-reference-policy-checks-suggestion-confirm-audience-claim-type"></a>

In the AWS Management Console, the finding for this check includes the following message:

```
Confirm audience claim type: The 'aud' (audience) claim key identifies the recipients that the JSON web token is intended for. Audience claims can be multivalued or single-valued. If the claim is multivalued, use a ForAllValues or ForAnyValue qualifier. If the claim is single-valued, do not use a qualifier.
```

In programmatic calls to the AWS CLI or AWS API, the finding for this check includes the following message:

```
"findingDetails": "The 'aud' (audience) claim key identifies the recipients that the JSON web token is intended for. Audience claims can be multivalued or single-valued. If the claim is multivalued, use a ForAllValues or ForAnyValue qualifier. If the claim is single-valued, do not use a qualifier."
```

**Resolving the suggestion**

The `aud` \(audience\) claim key is a unique identifier for your app that is issued to you when you register your app with the IdP and identifies the recipients that the JSON web token is intended for\. Audience claims can be multivalued or single\-valued\. If the claim is multivalued, use a `ForAllValues` or `ForAnyValue` condition set operator\. If the claim is single\-valued, do not use a condition set operator\.

**Related terms**
+ [Creating a role for web identity or OpenID Connect Federation \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_create_for-idp_oidc.html)
+ [Using multiple keys and values](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_multi-value-conditions.html#reference_policies_multi-key-or-value-conditions)
+ [Single\-valued vs\. multivalued condition keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_single-vs-multi-valued-condition-keys.html)