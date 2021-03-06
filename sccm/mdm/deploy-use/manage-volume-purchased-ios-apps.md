---
title: "Manage volume-purchased iOS apps | Microsoft Docs"
description: "Deploy, manage, and track licenses for apps you purchased through the iOS app store."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
caps.latest.revision: 18
caps.handback.revision: 0
author: mtillman
ms.author: mtillman
manager: angrobe
---
# Manage volume-purchased iOS apps with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*



 The iOS app store lets you buy multiple licenses for an app that you want to run in your company. This helps you reduce the administrative overhead of tracking multiple copies of apps that you bought.  

 System Center Configuration Manager helps you deploy and manage iOS apps that you bought through the program by importing the license information from the app store and tracking the number of the licenses that you have used.  

## Manage volume-purchased apps for iOS devices  
 You buy multiple licenses for iOS apps through the Apple Volume Purchase Program (VPP). This involves setting up an Apple VPP account from the Apple web site and uploading the Apple VPP token to Configuration Manager, which provides the following capabilities:  

-   Sync your volume purchase information with Configuration Manager.  

-   Apps that you bought are displayed in the Configuration Manager console.  

-   You can deploy apps, monitor these apps, and track the number of licenses for each app that has been used.  

-   Configuration Manager can help you reclaim licenses when required by uninstalling volume-purchased apps that you deployed to users.  

## Before you start  
 Before you begin, you'll need to get a VPP token from Apple and upload this to Configuration Manager.  

> [!IMPORTANT]  
>  -   Currently, each organization can have only one VPP account and token.  
> -   Only the Apple Volume Purchase Program for Business is supported.  
> -   After you associate an Apple VPP account to Intune, you cannot subsequently associate a different account. For this reason, make sure that more than one person has the details of the account that you use.  
> -   If you previously used a VPP token with a different MDM product in your existing Apple VPP account, you must generate a new one to use with Configuration Manager.  
> -   Each token is valid for one year.  
> -   By default, Configuration Manager syncs with the Apple VPP service twice a day to ensure that your licenses are synced with Configuration Manager.  
>   
>      Only changes to your licenses are synced. But, once every seven days, a full sync will be performed.  
>   
>      When you choose **Sync** to do a manual sync, this will always do a full sync.  
> -   If you need to recover or restore you Configuration Manager database, we recommend that you do a manual sync afterwards to ensure that your synced license data is up to date.  
> -   Although you can deploy iOS volume-purchased apps to user or device collections, VPP apps that you deploy to a device without a user (for instance, a device you enrolled without user affinity using the Device Enrollment Program (DEP) or Apple Configurator) will not be installed.  

 Additionally, you must have imported a valid Apple Push Notification service (APNs) certificate from Apple to let you to manage iOS devices, including app deployment. For more information, see [Set up iOS hybrid device management](enroll-hybrid-ios-mac.md).  

## Step 1 - To get and upload an Apple VPP token  

1.  In the Configuration Manager console, choose **Administration** > **Cloud Services** > **Apple Volume Purchase Program Tokens**.   

3.  On the **Home** tab, in the **Apple Volume Purchase Program Tokens** group, choose **Add Apple Volume Purchase Program Token**.  

4.  On the **General** page of the **Add Apple Volume Purchase Program Token** wizard, configure the following:   

    -   **Name** - Enter a name for this token as it will be displayed in the Configuration Manager console.  

    -   **Token** - Choose **Browse**, and then choose the VPP token that you downloaded from the Apple web site.  

         Choose the **See Apple VPP account** link, and if you haven't already, sign up for the business or education volume purchase program. After you are signed up, download the Apple VPP token for your account.  

    -   **Description** - Optionally, enter a description that will help you identify this VPP token in the Configuration Manager console.  

    -   **Assigned categories to improve searching and filtering** - Optionally, you can assign categories to the VPP token to make it easier to search for in the Configuration Manager console.  

5.  Choose **Next**, and then finish the wizard.  

From the **Apple Volume Purchase Program Tokens** node, you can now view information about the Apple VPP token including when it was last updated, when it will expire, and when it was last synced.

You can fully sync the data held by Apple with Configuration Manager at any time by choosing **Sync** on the **Home** tab in the **Sync** group.  

## Step 2 - Deploy a volume-purchased app  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **License Information for Store Apps**.  

3.  Choose the app that you want to deploy, and then, in the **Home** tab, in the **Create** group, choose **Create Application**.
The Configuration Manager application that is created has the Windows Store for Business app. You can then deploy and monitor this application as you would any other Configuration Manager application.

    > [!IMPORTANT]  
    > You must choose a deployment purpose of **Required**. Available installations are not currently supported.

 When you deploy the app, a license is used by each user who installs the app.  

 To reclaim a license, you must change the deployment action to **Uninstall**. The license will be reclaimed after the app uninstalls.  

## Step 3 - Monitor iOS VPP apps  
 The **License Information for Store Apps** node of the **Software Library** workspace displays information about your volume-purchased iOS apps. The information includes the total number of licenses that you own for each app and the number that have been deployed.

 You can also monitor the license usage of all VPP apps that you bought by using the **Apple Volume Purchase Program apps for iOS with license counts** report.  

 This report shows the name of each application together with the total number of licenses that you bought, the number of licenses available, and more.  

 For help with running Configuration Manager reports, see [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md).  
