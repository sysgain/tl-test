# Pre-Deployment Steps for Cold Chain Solution

## Table of Contents

[Overview](#Overview)

[Pre-Requisites](#Pre-requisites)

[Exercise 1: Create Azure Active Directory Application](#exercise-1-create-azure-active-directory-application)

[Exercise 2: Create Session ID](#exercise-2-create-session-id)
 
## Overview

Secure Cold Chain solution for Pharma addresses the challenges and concerns of the pharmaceutical companies, by providing near real-time tracking of the temperature sensitive consignments in a transparent and immutable manner throughout the supply chain, by combining IoT and Blockchain. The solution provides actionable insights for all the stakeholders through real time data capture, comprehensive analytics and immutable access with increased granularity (product, box, carton, or pallet level), thus helping in achieving business transformation and reaping the associated benefits.
To deploy the Cold Chain solution you need to perform few pre-deployment steps like creating Azure AD application and creating Session ID.
### Scenario and Objectives

You were asked to Create Azure AD application and Sessiom ID.

After completing this lab, you will be able to:

*	Create Azure AD application
*	Create session ID

## Pre-Requisites

* Azure portal access with Owner permission.

**Note:** You should have access to Azure portal with Owner permission to complete this Training Lab

## Exercise 1: Create Azure Active Directory Application

**Scenario**

This exercise explains about how to create Azure AD application.

The main tasks for this exercise are as follows:

### Task 1: Create Azure Active Directory Application

#### Integrating Applications with Azure Active Directory
    
Any application that wants to use the capabilities of Azure AD must first be registered in an Azure AD tenant. This registration process involves giving Azure AD details about your application, such as the URL where it’s located, the URL to send replies after a user is authenticated, the URI that identifies the app, and so on. 
    
#####   To Register a new Application using the Azure Portal 

1.	Sign in to the **Azure portal.**
2.	In the left-hand navigation pane, click the **Azure Active Directory(symbol)** service, click **App registrations,** and click **+ New application registration.**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d1.png)

1. When the **Create** page appears, enter your application's registration information:
  - **Name**: Enter the application name
  - **Application type:**
      * Select "Web app / API" for client applications and resource/API applications that are installed on a secure server. This setting is used for OAuth confidential web clients and public user-agent-based clients. The same application can also expose both a client and resource/API.
  - **Sign-On URL:** For "Web app / API" applications, provide the base URL of your app. For example, **https://localhost** might be the URL for a web app running on your local machine. Users would use this URL to sign in to a web client application.
  
4.When finished, click **Create.**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d2.png)

#####   To add Application Credentials or Permissions to Access Web APIs

1. Click the **Azure Active Directory** service, click **App registrations,** and then find/click the application you want to configure.
2. You are taken to the application's main registration page, which opens the **Settings** page of the application. To add a secret key for your web application's credentials:
3. Click the **Keys** section on the **Settings** page.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d3.png)

4. Add a description for your key and Select duration, click **Save**. 

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d4.png)   
    
5. The right-most column will contain the key value, after you save the configuration changes. **Be sure to copy the key** for use in your client application code, as it is not accessible once you leave this page.  

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d4-1.PNG)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d5.png)

#####   To get Tenant ID

1. Select **Azure Active Directory.**
2.	To get the tenant ID, select for your **Azure AD Properties tenant** and **Copy** the **Directory ID**. This value is your **tenant ID.**
3. **Note down** the Copied **Directory ID** which is highlighted in the below figure, this will be used while deploying the **ARM template.**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d6.png)

#####   To get application ID and Authentication Key

1. From **App registrations** in **Azure Active Directory, select** your **application.**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d7.png)

2. **Copy** the **Application ID** and **object ID.** The application ID value is referred as the **client ID.**
3. **Note down** the Copied **Application ID** and **object ID** which is highlighted in the below figure, this will be used while deploying the **ARM template.**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d8.png)

**Result:** After completing this exercise, you should have successfully created Azure AD application.

## Exercise 2: Create Session ID

**Scenario**

This exercise explains about how to create session ID.

The main tasks for this exercise are as follows:

### Task 1: Create session ID

1.	Use the below **URL to generate GUID.**

<https://www.guidgenerator.com/>

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d9.png)

2. Click **Generate some GUIDs!** This will generate **GUID** in Results box. 
    
3.	**Copy** and **Note down** the generated GUID which is highlighted in the below figure, this will be used while deploying the **ARM template.**  

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d10.png)

**Result:** After completing this exercise, you should have successfully created Session ID.