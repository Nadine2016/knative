---

copyright:
  years: 2020
lastupdated: "2020-04-13"

keywords: knative

subcollection: knative

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: target="_blank" .external}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:gif: data-image-type='gif'}

# Troubleshooting tips
{: #kn-troubleshoot}

Use the troubleshooting tips to learn how to troubleshoot Knative service.
{: shortdesc}

## Set up an IAM policy for Coligo

Whenever you are using an IBM Cloud account to create or use a Project that is not owned by you, you must have proper system roles. To perform operations with the Project, the right Access Policy must be applied to you as a user by the Account Owner or by someone with Admin access to the IBM Cloud Account in question. 

The following steps must be performed by the Account Owner or someone with Admin access to the Cloud Account. 
{: note}

For more information, see [Understanding IAM](https://cloud.ibm.com/docs/iam?topic=iam-getstarted) and [Best Practices](https://cloud.ibm.com/docs/iam?topic=iam-account_setup){: external}.

### Assigning access to an existing Project 

1. Determine if the user exists in IAM Access. Go to the [Manage Access Users](https://cloud.ibm.com/iam/users){: external} page and search for the user. 
  * To add a new user, click `Invite users`. 
  * If the user already exists in the list, from the List of Actions menu, select the `Assign Access` option. 
2. Once the user exists in IAM, assign the user access to the Project. From the `Assign users additional access` section on the `IAM Services` tile:
    1. For `What type of access to you want to assign`, from the dropdown, select `Functions`.  
    2. For `in`, select the `Resource Group` from the dropdown where the Project exists.  If you select `All Resource Groups`, the user is given access to all Projects in all Resource groups. 
    3. For `Region`, specify the region from the dropdown. For example, specify  `Dallas` as this only works for the `US-South` region. 
    4.  For `Platform Access`, select `Viewer` as the role. 
    5.  For `Service Access`, select `Reader` as the role.
    6.  For `Resource Group Access`, select `Viewer` as the role. 
    7.  Click `Add` to add the roles.
3.  Review the Access Summary information and modify if needed.  
4.  When ready, click `Invite` to assign the specified access to the user. (?? Invite for new users?  Assign for existing??) 

### Assigning a user permissions to create Projects

To create Projects, a user must have an Administrative role in the Project.  
1. Determine if the user exists in IAM Access. Go to the [Manage Access Users](https://cloud.ibm.com/iam/users){: external} page and search for the user. 
  * To add a new user, click `Invite users`.  
  * If the user already exists in the list, from the List of Actions menu, select the option to `Assign Access`. 
2. Once the user is in IAM, you can assign an Administrative role to the user to enable the user to create Projects.  From from the `Assign users additional access` section on the `IAM Services` tile:
    1. For `What type of access to you want to assign`, from the dropdown, select `Functions`.  
      * For `in`, select the `Resource Group` from the dropdown where the Project exists.  If you select `All Resource Groups`, the user is given access to all Projects in all Resource groups.   
    2. For `Region`, specify the region from the dropdown. For example,  `Dallas` as this only works for the `US-South` region. 
    3.  For `Platform Access`, select `Administrator` as the role. 
    4.  For `Service Access`, select `Reader` as the role.
    5.  For `Resource Group Access`, select `Viewer` as the role. 
    6.  Click `Add` to add the roles.
3.  Review the Access Summary information and modify if needed.  
4.  When ready, click `Assign` to assign the specified access to the user.

