---
title: Azure Analysis Service ID cannot be specified for Azure Analysis Service role member
categories: []
tags: []
---

After trying to configure Role Level Security as described in the following article:

https://docs.microsoft.com/de-de/power-bi/desktop-tutorial-row-level-security-onprem-ssas-tabular

We experienced the following issue when we were trying to add any Azure AD user.

ID cannot be specified for Azure Analysis Service role member: user@domain.com



The solution was to switch to Integrated workspace and to deploy the model again.
https://docs.microsoft.com/en-us/analysis-services/tabular-models/workspace-database-ssas-tabular

Also make sure, when you want to user Azure AD as Identity Provider, that you user user@domain.com and use **Add External
**https://docs.microsoft.com/en-us/azure/analysis-services/analysis-services-database-users#to-add-or-manage-roles-and-users-in-visual-studio
