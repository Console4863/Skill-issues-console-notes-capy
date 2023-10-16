Link: https://www.tp-link.com/no/support/faq/2678/


# How to configure the NPS to manage RADIUS authentication with Omada Controller

Configuration Guide

Updated 06-27-2022 03:46:57 AM ![](https://static.tp-link.com/res/images/icons/article-views.png)_97075_

**This Article Applies to:** 

NPS on the Windows Server can work as RADIUS Server to manage RADIUS authentication with Omada Controller. As shown below, NPS can perform centralized authentication for wireless connections when acting as a RADIUS Server. This article will introduce you how to configure the NPS on the Windows Server 2012 R2 to work with Omada Controller.

![](https://static.tp-link.com/image001_1572250344805p.jpg)

By default, there are no network services in the Windows Server. So we need to add roles manually to implement the corresponding function. Besides NPS, we also need to install Active Directory Domain Services and Active Directory Certificate Services. Only in this way, NPS can authenticate user accounts. Therefore, we will describe it in the following steps:

· Install Active Directory Domain Service

· Install Active Directory Certificate Services

· Install Network Policy and Access services

· Create Group and User

· Configure RADIUS Clients and Network Policies

· Example of the External RADIUS Server.

**I.** **Install Active Directory Domain Services**

NPS must be registered in Active Directory so that it has permission to read the dial-in properties of user accounts during the authorization process. So we need to install Active Directory DS and promote it to a domain controller first.

![](https://static.tp-link.com/image002_1572250360928y.jpg)

**II.** **Install Active Directory Certificate Services**

Besides Active Directory DS, we need to install Active Directory Certificate Services. After installation, it will issue a certificate to Active Directory DC and Windows Server.

Note: If it doesn’t issue the certificate to Windows Server, we need to apply for a certificate for the Windows Server from the CA to ensure SSL encryption.

![](https://static.tp-link.com/image003_1572250370667j.jpg)

**III.** **Install Network Policy and Access services**

Go to Server Manager to install Network Policy and Access Services. After that, we should register the NPS in Active Directory DS so that it has permission to access user account and information while processing connection requests.

![](https://static.tp-link.com/image004_1572250380746z.jpg)

**IV.** **Create Group and User**

After installing Active Directory DS, please go to the Active Directory Administrative Center to create a group and add new users to this group. (These users are used to login and access the internet.)

![](https://static.tp-link.com/image005_1572250390155o.jpg)

Don’t forget to change the dial-in property to “Control access through Network Policy Server”, to allow users of this group to access the network through the NPS network policy.

![](https://static.tp-link.com/image006_1572250398159l.jpg)

**V.** **Configure RADIUS Clients and Network Policies**

RADIUS client can create RADIUS access request messages and forward them to the RADIUS server. To configure NPS as a RADIUS server, we must configure RADIUS clients and network policy.

![](https://static.tp-link.com/image007_1572250407106m.jpg)

To add the EAP as a client, enter the device’s IP address and give it the friendly name “tplink_nps” and manually enter a “Shared Secret”. The Shared Secret is used to verify that the RADIUS client is allowed to process auth-requests through the RADIUS server.

Note: The Radius Client role is transferred from EAP to Omada Controller since Controller 3.1.4.

To compatible with WPA-Enterprise and portal RADIUS, we should enable “Unencrypted authentication (PAP, SPAP)” when configuring the network policies.

![](https://static.tp-link.com/image008_1572250416712b.jpg)

**VI.** **Example of the External RADIUS Server**

After installed and configured on the Windows Server, NPS can work as a RADIUS Server. Here we take the External RADIUS Server portal as an example, use NPS to authenticate users who connect to the portal SSID.

![](https://static.tp-link.com/image009_1572250426336f.jpg)

· RADIUS Server IP: IP address of the Windows Server；

· RADIUS Port: The default port is 1812;

· RADIUS Password: It is the shared secret that we input the RADIUS Client page.

After configuring the portal, we can connect to the portal SSID, input the username and password, and then we will be able to access the internet.

![](https://static.tp-link.com/image010_1572250436216p.png)