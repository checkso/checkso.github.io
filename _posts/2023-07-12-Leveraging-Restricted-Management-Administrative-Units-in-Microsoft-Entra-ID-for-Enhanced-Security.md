---
title: Leveraging Restricted Management Administrative Units in Microsoft Entra ID for Enhanced Security
date: 2023-07-12
categories: [Microsoft, Entra ID] 
tags: [Microsoft, Entra ID, Administrative Units, Conditional Access Policies]
---

Security and granular control are cornerstones of any sound IT strategy. 
This is especially true when managing user access in cloud platforms like Microsoft Entra ID (formerly Azure AD). 
Today, we'll explore how Restricted Management Administrative Units can help you fine-tune your access management and add an extra layer of security.

## The Challenge

Before we delve into the solution, let's outline the challenge we face. In the past, when managing Microsoft Entra Conditional Access Policies, you could use groups to exclude certain users, but this approach had its drawbacks. 
Specifically, the lack of granular controls made it difficult to ensure that only a designated subset of administrators could manage the group members. 
This becomes even more concerning when you have various global teams - the broader the geographical spread, the greater the potential for inadvertent or inappropriate access.

## The Solution: Restricted Management Administrative Units

Responding to this crucial need for more controlled and secure administrative privileges, Microsoft Entra ID introduced Restricted Management Administrative Units. This feature facilitates the protection of specific objects within your tenant, restricting their modification to a defined group of administrators.

In practice, this allows you to comply with stringent security and compliance requirements without stripping tenant-level role assignments from your administrators. A heightened level of control is now achievable, providing both a practical solution and peace of mind.

One of the standout benefits is the ability to create Restricted Administrative units, to which you can assign a subset of admin accounts. 
You can then add specific groups to these units—for instance, all break glass accounts—and subsequently incorporate this group into your conditional access policy. 
This increased granularity in managing permissions offers a more secure and efficient means of managing global teams and critical accounts.

## What Else?

Let's delve a little deeper and explore some additional ways you can utilize this feature for enhanced access management within your tenant, right from Microsoft.


- You want to protect your C-level executive accounts and their devices from Helpdesk Administrators who would otherwise be able to reset their passwords or access BitLocker recovery keys. You can add your C-level user accounts in a restricted management administrative unit and enable a specific trusted set of administrators who can reset their passwords and access BitLocker recovery keys when needed.
- You're implementing a compliance control to ensure that certain resources can only be managed by administrators in a specific country. You can add those resources in a restricted management administrative unit and assign local administrators to manage those objects. Even Global Administrators won't be allowed to modify the objects unless they assign themselves explicitly to a role scoped to the restricted management administrative unit (which is an auditable event).
- You're using security groups to control access to sensitive applications in your organization, and you don’t want to allow your tenant-scoped administrators who can modify groups to be able to control who can access the applications. You can add those security groups to a restricted management administrative unit and then be sure that only the specific administrators you assign can manage them.

[Link to Microsoft Learn](https://learn.microsoft.com/en-us/azure/active-directory/roles/admin-units-restricted-management)
