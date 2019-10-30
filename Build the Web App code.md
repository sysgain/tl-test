# Build the Web App code for Secure Cold Chain Solution

## Table of Contents

[Overview](#Overview)

[Pre-Requisites](#Pre-requisites)

[Exercise 1: Create Bing Map API Key](#exercise-1-create-bing-map-api-key)

[Exercise 2: Build UI Code](#exercise-2-build-ui-code)

[Exercise 3: Uploading the Built UI code to Web Application](#exercise-3-uploading-the-built-ui-code-to-web-application)

## Overview

Secure Cold Chain solution for Pharma addresses the challenges and concerns of the pharmaceutical companies, by providing near real-time tracking of the temperature sensitive consignments in a transparent and immutable manner throughout the supply chain, by combining IoT and Blockchain. The solution provides actionable insights for all the stakeholders through real time data capture, comprehensive analytics and immutable access with increased granularity (product, box, carton, or pallet level), thus helping in achieving business transformation and reaping the associated benefits.

### Scenario and Objectives

You were asked to create Bing Maps API key, build the UI code and upload the built code to web application.

After completing this lab, you will be able to:

* Create Bing Maps API key

* Understand the process of bulding the nodejs code

* Understand the process of uploading the built UI code to web application

## Pre-Requisites

* Azure Portal access with Owner permission.
* You need to have the local copy of the Secure Cold Chain repository. You can download/clone the same from the below url
  https://github.com/SecureColdChain/Wipro-Ltd-ColdChain

* You need to complete the following labs before attempting this lab
  Pre-Deployment Steps for Cold Chain Solution
  Deploying the Cold Chain Solution ARM template
  Post-Deployment Steps for Cold Chain Solution

**Note:** You should have access to Azure portal with Owner permission to complete this Training Lab

## Exercise 1: Create Bing Map API Key

**Scenario**

This exercise explains about how to create a Bing map API key

The main tasks for this exercise are as follows:

1. Create Bing Map API key

### Task 1: Create Bing Map API Key

1. In Azure portal click on Create a resource.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/b1.png)
2. Search for “bing maps” as show below and click on Bing Maps API for Enterprise.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/b2.png)
3. Click on Create.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/b3.png)
4. Fill all the required details as shown below and click on Create.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/b4.png)
5. Go the resource group and Click on Bing map resource 

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/b5.png)
6. Click on the Key Management and copy the masterkey this value you need to use for BingApiKey

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/b6.png)

 Here you can updated the details:

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d70.png)

## Exercise 2: Build UI Code

**Scenario**

This exercise explains about how to build the nodejs code.

### Task 1: Building the Web App code

Follow the below steps to build web application UI code to point to the deployed resources 

1.	Open the **ProjectTitanUICode** from **UI WebApp** folder from the **ColdChain** folder. 

 **Note:** Clone the cold-chain repository to your local system and perform the below steps

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d61.png)

1. Open the **src** folder from **ProjectTitanUICode** folder.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d62.png)

3.	Open environment folder and update the values of **environment.prod** file.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d63.png)

4.	Update the values **API_Endpoint, SAS_Token,blobAccessUrl,storageUrl, client_id,web3_password,contractAddress,HttpProvider,gasLimit and BingApiKey**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d64.png)

5. You can take all the resource values from the ARM template output section
![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d128.png) 

6.	You can get all the values from the Azure portal as shown below and use the same contract address which you have copied in the earlier step (**5.1. Deploying smart contract and getting the Contract Address**)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d65.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d66.png)

7.Click on **Storage Account -> Shared access signature.**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d67.png)

8. Click on **Generate SAS and connection string** button. Copy the **SAS token** and **Blob Access URL** and update into **environment.prod.ts** file.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d68.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d69.png)

Here you can updated the details:
 
![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d70.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d127.png)

9. After updating the **environment.prod.ts** click on open **Node.js command prompt** window and go to the ProjectTitanUICode location i.e. you web application code location as shown in the following screenshots.

**NOTE:** make sure that you have latest **node modules installed** and you have **Angular CLI** installed on your local machine

Command: **npm install -g @angular/cli**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d71.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d72.png)

10. Here we can **install npm**

Command: **npm install**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d73.png)

11.	Run the following command to build the code 

Command: **ng build –prod**

Note: Before running the above command make sure that you have installed Angular CLI.

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d74.png)

12. After successful build, you will get the folder called **dist**

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d75.png)

13.	Open **AngularFrontEnd** from the **dist folder,** add the web.config(download it from here ) to the **AngularFrontEnd** and select all the files then zip them. 

**Note**: Download the Web.config file from the repository

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d76.png)

## Exercise 3: Uploading the Built UI code to Web Application

**Scenario**

This exercise explains about how to upload the UI code to web application using Azure portal.

### Task 1: Uploading the Built UI code to Web Application

1. Open kudu tool to upload the built web application code to the web app. You can open the Kudu tool by adding the scm in the web App URL as shown below 

Ex: <https://webapikowgh.scm.azurewebsites.net)>

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d77.png)

2. Click on **Tools** dropdown list and click **Zip Push Deploy** to push the zipped web app code as shown below.

**Note:** Remove the existing files before you push new code. 

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d78.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d79.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d80.png)

![alt text](https://github.com/SecureColdChain/Wipro-Ltd-ColdChain/blob/master/Documentation/images/d81.png)
