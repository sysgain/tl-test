# Deploy the Cold Chain Solution ARM template

## Table of Contents

[Overview](#Overview)

[Pre-Requisites](#Pre-requisites)

[Exercise 1: Deploy the Secure Cold Chain Solution](#exercise-1-deploy-the-secure-cold-chain-solution)

## Overview

Secure Cold Chain solution for Pharma addresses the challenges and concerns of the pharmaceutical companies, by providing near real-time tracking of the temperature sensitive consignments in a transparent and immutable manner throughout the supply chain, by combining IoT and Blockchain. The solution provides actionable insights for all the stakeholders through real time data capture, comprehensive analytics and immutable access with increased granularity (product, box, carton, or pallet level), thus helping in achieving business transformation and reaping the associated benefits.

### Scenario and Objectives

In this lab you were asked to deploy the Secure Cold Chain Solution using ARM template.

After completing this lab, you will be able to understand:

*	deploying ARM template in Azure portal

*	deploying ARM template using Azure CLI

*    terminology  of ARM template like input parameters ,output parameters and variables.

## Pre-Requisites

* Azure Portal access with Owner permission.
* You need to complete the lab **Pre-Deployment Steps for Cold Chain Solution**

**Note:** You should have access to Azure portal with Owner permission to complete this Training Lab

## Exercise 1: Deploy the Secure Cold Chain Solution

**Scenario**

This exercise explains about how to deploy Secure Cold Chain solution using ARM template in Azure portal.

The main tasks for this exercise are as follows:

### Task 1: Deploy ARM Template

Azure Resource Manager allows you to provision your applications using a declarative template. In a single template, you can deploy multiple services along with their dependencies. The template consists of JSON and expressions that you can use to construct values for your deployment. You use the same template to repeatedly deploy your application during every stage of the application lifecycle.
Resource Manager provides a consistent management layer to perform tasks through Azure PowerShell, Azure CLI, Azure portal, REST API, and client SDKs.
Resource manager provides the following features:
-	Deploy, manage, and monitor all the resources for your solution as a group, rather than handling these resources individually.
-	Repeatedly deploy your solution through the development lifecycle and your resources are deployed in a consistent state.
-	Manage your infrastructure through declarative templates rather than scripts.
-	Define the dependencies between resources so they're deployed in the correct order.
-	Apply access control to all services in your resource group because Role-Based Access Control (RBAC) is natively integrated into the management platform.
-	Apply tags to resources to logically organize all the resources in your subscription.

####    ARM Template Deployment Using Azure Portal

1.	Click the below **Git hub** URL.

https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/maintemplate.json

2. **Copy** the raw template and **paste** in your **Azure Portal** for template deployment.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d13.png)
    
**To deploy a template for Azure Resource Manager, follow the below steps.**
1.	Go to **Azure portal.**
2.	Navigate to **Create a resource (+)**, search for **Template deployment.**
3.	Click **Create** button and click **Build your own Template in the editor** as shown in the following figure.
![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d13-1.PNG)
![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d13-2.PNG)
![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d14.png)

4.	The **Edit template** page is displayed as shown in the following figure.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d15.png) 

5.	**Replace / paste** the template and click **Save** button.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d16.png)

6. The **Custom deployment** page is displayed as shown in the following figure. 

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d17.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d18.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d19.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d20.png)

####   Inputs

These parameter values enable you to customize the deployment by providing values. These parameters allow to choose the solution type, region and AD Application details. 

**Parameters for Basic Solution:**

If you want to deploy the **Basic Solution** you must enter the values for the parameters mentioned in the **Exercise 1, Task 3**.

For **basic solution,** enter the parameters as shown below. 

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/1.PNG)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/2.PNG)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/3.PNG)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/4.PNG)

**Parameters for Standard Solution**

If you want to deploy the **standard solution** you must enter the below parameters as shown in the screens.

For **standard solution,** select new values for **numBlockMakers as 2, apiManagement as YES/NO** and keep the default values for other parameters. 

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/5.PNG)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/6.PNG)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/7.PNG)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/8.PNG)

**Parameters for Premium solution:**

If you want to deploy the **Premium solution** you must enter the below parameters as shown in the screens.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/9.PNG)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/10.PNG)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/11.PNG)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/12.PNG)

Once all the parameters are entered, check in the **terms and conditions** check box and click **Purchase.**

After the successful deployment of the ARM template, the following **resources** are created in a **Resource Group.**

1.	App Service
-	Function App
-	WebApp
2.	App Service Plan
-	App service plan
-	Consumption Plan
3.	Application Insights
4.	Automation Account
5.	Availability Set
6.	Azure Cosmos DB Account
7.	IoT Hub
8.	Load Balancer
9.	Log Analytics Workspace
10.	Network Interface
11.	Network Security Group
12.	Public Ip Address
13.	RUN Book
14.	OMS Solution
15.	SQL Database
16.	SQL Server
17.	Storage Account
18.	Stream Analytics Job
19.	Virtual Machine
20.	Virtual Network
21. Quorum Blockchain setup

The above resources are deployed for **Basic Solution.**

Once the solution is deployed successfully, navigate to the **resource group** to view the list of resources that are created as shown below.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d33.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d34.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d35.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d36.png)

#####   Outputs
Go to **Resource Group** -> Click **Deployments** then click on **Microsoft.Template** after that click on **Outputs**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d37.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d38.png)

**Result:** After completing this exercise, you should have successfully deployed Secure Cold Chain Solution.