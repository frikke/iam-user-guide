# IAM console search<a name="console_search"></a>

Use the IAM console search page as a faster option for finding IAM resources\. You can use the console search page to locate access keys related to your account, IAM entities \(such as users, groups, roles, identity providers\), policies by name, and more\.

The IAM console search feature can locate any of the following:
+ IAM entity names that match your search keywords \(for users, groups, roles, identity providers, and policies\)
+ Tasks that match your search keywords

The IAM console search feature does not return information about IAM Access Analyzer\.

Every line in the search result is an active link\. For example, you can choose the user name in the search result, which takes you to that user's detail page\. Or you can choose an action link, for example **Create user**, to go to the **Create User** page\.

**Note**  
Access key search requires you to type the full access key ID in the search box\. The search result shows the user associated with that key\. From there you can navigate directly to that user's page, where you can manage the access key\.

## Using IAM console search<a name="using_search"></a>

Use the **Search** page in the IAM console to find items related to that account\. 

**To search for items in the IAM console**

1. Follow the sign\-in procedure appropriate to your user type as described in the topic [How to sign in to AWS](https://docs.aws.amazon.com/signin/latest/userguide/how-to-sign-in.html) in the *AWS Sign\-In User Guide*\.

1. On the **Console Home** page, select the IAM service\.

1. In the navigation pane, choose **Search**\. 

1. In the **Search** box, type your search keywords\.

1. Choose a link in the search results list to navigate to the corresponding part of the console\. 

## Icons in the IAM console search results<a name="search_icons"></a>

The following icons identify the types of items that are found by a search:


****  

| Icon | Description | 
| --- | --- | 
|  ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/search_user.png)  | IAM users | 
|  ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/search_group.png)  | IAM groups | 
|  ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/search_role.png)  | IAM roles | 
|  ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/search_policy.png)  | IAM policies | 
|  ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/search_action.png)  | Tasks such as "create user" or "attach policy" | 
|  ![\[Image NOT FOUND\]](http://docs.aws.amazon.com/IAM/latest/UserGuide/images/search_delete.png)  | Results from the keyword delete | 

## Sample search phrases<a name="search_phrases"></a>

You can use the following phrases in the IAM search\. Replace terms in italics with the names of the actual IAM users, groups, roles, access keys, policies, or identity providers that you want to locate\.
+ ***user\_name*** or ***group\_name* ** or ***role\_name*** or ***policy\_name*** or ***identity\_provider\_name***
+ ***access\_key***
+ **add user *user\_name* to groups** or **add users to group *group\_name***
+ **remove user *user\_name* from groups**
+ **delete *user\_name*** or **delete *group\_name*** or **delete *role\_name***, or **delete *policy\_name***, or **delete *identity\_provider\_name***
+ **manage access keys *user\_name***
+ **manage signing certificates *user\_name***
+ **users**
+ **manage MFA for *user\_name***
+ **manage password for *user\_name***
+ **create role**
+ **password policy**
+ **edit trust policy for role *role\_name***
+ **show policy document for role *role\_name***
+ **attach policy to *role\_name***
+ **create managed policy**
+ **create user**
+ **create group**
+ **attach policy to *group\_name***
+ **attach entities to *policy\_name***
+ **detach entities from *policy\_name***