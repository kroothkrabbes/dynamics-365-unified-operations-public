---
# required metadata

title: Dynamics 365 for Operations versions and update policy | Microsoft Docs
description: This topic describes the E-Commerce Platform SDK.
author: kfend
manager: AnnBe
ms.date: 2015-12-04 23:12:08
ms.topic: article
ms.prod: 
ms.service: Dynamics365Operations
ms.technology: 

# optional metadata

# keywords: 
# ROBOTS: 
audience: Developer
# ms.devlang: 
ms.reviewer: kfend
ms.suite: Released- Dynamics AX 7.0.0
# ms.tgt_pltfrm: 
ms.custom: 18101
ms.assetid: cb9328b8-b382-4e55-875f-e98ce1f4d094
ms.region: Global
# ms.industry: 
ms.author: meeram

---

# Dynamics 365 for Operations versions and update policy

This topic describes the E-Commerce Platform SDK.

**Purpose: The** E-Commerce Platform SDK consist of the following components:

-   Framework
-   Controls
-   Publishing (only supported in version 1661 and higher : [Support for Service to Service authentication in Retail Server](https://community.dynamics.com/ax/b/axforretail/archive/2016/09/24/support-for-service-to-service-authentication-in-retail-server))
-   Sample ASP.net web site

## Use the sample asp.net website
### Use the RetailSDK to create the sample asp.net website

1.  Open Visual Studio in Admin mode. This is necessary for publishing to the inetpub folder.
2.  Open C:\\Microsoft Dynamics AX70\\RetailSdkOnlineStoreOnlineStore.sln contains all the framework components.
3.  The sample online store is available at C:\\Microsoft Dynamics AX70\\RetailSdkSampleExtensionsOnlineStore.
4.  Compile and Publish the web storefront, from within Visual Studio.
5.  Update the path of the RetailStorefrontWebSite from IIS Manager.
    1.  Please note RetailStorefrontWebSite created by the default setup points to C:\\Microsoft Dynamics AX70\\Retail Store Front\\Package.
    2.  However, the publishing of the web storefront from RetailSDK will drop the files at C:\\inetpub\\RetailWeb\\Storefront.
    3.  Hence, the physical path of the RetailStorefrontWebSite must be updated to point to “C:\\inetpub\\RetailWeb\\Storefront” to access web storefront on the same ports as before. Another option would be to create a new website and have that point to the inetpub location.

6.  Browse to <http://localhost:55080> or access the https://usnconeboxax1ecom.cloud.onebox.dynamics.com/en/ to see a test asp.net web site.

### Enabling anonymous access

E-Commerce websites need to enable anonymous access. This is available as a web.config in the Retail Server web.config under app settings. Please ensure this is enable to have the web site work. &lt;add key="IsAnonymousEnabled" value="true" /&gt;

### Externally accessing the ASP.net website

The following configuration changes will be required if either of these applies:

-   if you are accessing web storefront from within a browser that is not on the same box as the Ecommerce server
-   if the ecommerce server and retail server are on two different boxes

You will need to update the “retailServerUrl” inside web.config of the RetailStorefrontWebSite. The following two fields will need to be updated to use the machine name instead of local host:

-   retailServerUrl=<http://localhost:35080/RetailServer/V1>
-   &lt;add key="RetailServerRoot" value="<http://localhost:35080/RetailServer/V1>" /&gt;

If you are accessing the web storefront over https, then you will need to update the above urls to the https equivalent.

### Operating unit or channel configuration

The E-Commerce web site will operate on an operating unit number(channel) specified in the web.config. To change it, change the OU \# below. Note that Fabrikam is “077” in the demo data. You will need to update the “retailServerUrl” inside web.config of the RetailStorefrontWebSite. The following two fields will need to be updated to use the machine name instead of local host:

-   <ecommerceControls productUrlFormat="/Pages/ProductDetails/ProductDetails.aspx?itemId={0}" retailServerUrl="http://localhost:35080/RetailServer/V1" operatingUnitNumber="068">

-   <add key="OperatingUnitNumber" value="068" />

## Configure authentication providers
### Authentication providers that you are using

The E-Commerce platform uses OpenID as the mechanism for authentication. You can register any OpenID provider of your choice to the tables below to make this work. You can then login to test as needed.

1.  Edit the web.config and change it to below.

        redirectUrl=https://usnconeboxax1ecom.cloud.onebox.dynamics.com/en/Pages/OauthV2Redirect/OauthV2Redirect.aspx

    The subsequent steps should only be done to register additional providers.

2.  The Retail Shared Parameters-&gt; Open ID Providers form can be used to register additional providers as below. [![ECommerce1](./media/ecommerce1-1024x430.png)](./media/ecommerce1.png)
3.  Run distribution schedule 1110.

