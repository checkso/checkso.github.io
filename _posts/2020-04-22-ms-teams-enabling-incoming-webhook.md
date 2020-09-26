---
title: MS Teams - Enabling Incoming Webhook
date: 2020-04-22 22:00:00 +0000
categories:
- Teams
tags:
- Incoming Webhook
- 3rd Party Apps
- Teams

---
In our tenant we have all 3rd Party Apps within Microsoft Teams **disabled**. We wanted to use the "Incoming Webhooks" App, but couldn't add it as it was not shown.

After some discussions with the Microsoft Support, we recevied the following information:

_"Working with Engineering Team we have confirmed that Incoming WebHooks App, although it is registered as Microsoft Corp distributed, the reason why it is considered a 3rd party App is because Microsoft does not own the Endpoints of it."_

So the "Incoming Webhook" App is registered as an 3rd Party App and needs to be allowed.

After allowing 3rd Party Apps, we were able to create the "Incoming Webhook", but it was not working with the error:

> Connectors have been disabled for client - SkypeSpaces. Please contact your administrator

![Error](/assets/images/error.png)

This can be related to three things:

**1. EWS Allow List**

If you use the EWS Allow List you need to add the agent string “__SkypeSpaces/1.0a$* SkypeSpaces/*__”.

In our case we didn't use the EWS Allow List

![](/assets/images/Get-OrgConfig1.png)

**2. Allow sideloading of external apps / Custom Apps**

![](/assets/images/customapps-1.png)

Within the Org-wide app settings "Allow interaction with custom apps" must be enabeld.

Also this was already enabled in our case.

**3. Organization Configuration - ConnectorsEnabled**

ConnectorsEnabled was set to **False** in our tenant. This can be set to **True** easily:

    Set-OrganizationConfig -ConnectorsEnabled $True

![](/assets/images/Get-OrgConfig.png)

After the change and waiting for the next day the Incoming Webhook was able to be added easily:

![](/assets/images/Webhook.png)
