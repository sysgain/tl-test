# Secure Cold Chain Solution - Leveraging IoT & Blockchain

## Table of Contents

[Overview](#Overview)

[Pre-Requisites](#Pre-requisites)

[Exercise 1: Deploy the Secure Cold Chain Solution](#exercise-1-deploy-the-secure-cold-chain-solution)

[Exercise 2: Configure Secure Cold Chain Solution to a working state](#exercise-2-configure-secure-cold-chain-solution-to-a-working-state)

[Exercise 3: Use the Secure Cold Chian Solution](#exercise-3-use-the-secure-cold-chian-solution)

[Exercise 4: Administer the Secure Cold Chain Solution](#exercise-4-administer-the-secure-cold-chain-solution)
 
## Overview

Secure Cold Chain solution for Pharma addresses the challenges and concerns of the pharmaceutical companies, by providing near real-time tracking of the temperature sensitive consignments in a transparent and immutable manner throughout the supply chain, by combining IoT and Blockchain. The solution provides actionable insights for all the stakeholders through real time data capture, comprehensive analytics and immutable access with increased granularity (product, box, carton, or pallet level), thus helping in achieving business transformation and reaping the associated benefits.

### Scenario and Objectives

You were asked to deploy the Secure Cold Chain Solution, configure the appication to a working state, use the application and administer the application.

After completing this lab, you will be able to:

*	Understand the different Azure IoT services like IoT Hub,Stream Analytics, Cosmos DB, SQL Database, Web App, Azure Functions, Quorum Blockchain Services

*	Security, High Availability and Disaster Recovery (HA & DR) strategies

*   Configuring the different devices for the IoT solution


## Pre-Requisites

* Azure Portal access with Owner permission.
    
* You need to have the following devices :
     1. Raspberry Pi3
     2. Teltonika TMT -250
     3. Rigado Cascade-500 IoT Gateway
     4. Beacons
* Familiar with Azure IoT services and Device configurations. 

**Note:** You should have access to Azure portal with Owner permission to complete this Training Lab

## Exercise 1: Deploy the Secure Cold Chain Solution

**Scenario**

This exercise explains about how to deploy Secure Cold Chain solution using ARM template in Azure portal.

The main tasks for this exercise are as follows:

1.	Create Azure Active Directory Application

2.	Create Session ID

3.	Deploy ARM Template

### Task 1: Create Azure Active Directory Application

#### Integrating Applications with Azure Active Directory
    
Any application that wants to use the capabilities of Azure AD must first be registered in an Azure AD tenant. This registration process involves giving Azure AD details about your application, such as the URL where it’s located, the URL to send replies after a user is authenticated, the URI that identifies the app, and so on. 
    
#####   To Register a new Application using the Azure Portal 

1.	Sign in to the **Azure portal.**
2.	In the left-hand navigation pane, click the **Azure Active Directory(symbol)** service, click **App registrations,** and click **+ New application registration.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d1.png)

3. When the **Create** page appears, enter your application's registration information:
  - **Name**: Enter the application name
  - **Application type:**
      * Select "Web app / API" for client applications and resource/API applications that are installed on a secure server. This setting is used for OAuth confidential web clients and public user-agent-based clients. The same application can also expose both a client and resource/API.
  - **Sign-On URL:** For "Web app / API" applications, provide the base URL of your app. For example, **https://localhost** might be the URL for a web app running on your local machine. Users would use this URL to sign in to a web client application.
  
4.When finished, click **Create.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d2.png)

#####   To add Application Credentials or Permissions to Access Web APIs

1. Click the **Azure Active Directory** service, click **App registrations,** and then find/click the application you want to configure.
2. You are taken to the application's main registration page, which opens the **Settings** page of the application. To add a secret key for your web application's credentials:
3. Click the **Keys** section on the **Settings** page.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d3.png)

4. Add a description for your key and Select duration, click **Save**. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d4.png)   
    
5. The right-most column will contain the key value, after you save the configuration changes. **Be sure to copy the key** for use in your client application code, as it is not accessible once you leave this page.  

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d4-1.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d5.png)

#####   To get Tenant ID

1. Select **Azure Active Directory.**
2.	To get the tenant ID, select for your **Azure AD Properties tenant** and **Copy** the **Directory ID**. This value is your **tenant ID.**
3. **Note down** the Copied **Directory ID** which is highlighted in the below figure, this will be used while deploying the **ARM template.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d6.png)

#####   To get application ID and Authentication Key

1. From **App registrations** in **Azure Active Directory, select** your **application.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d7.png)

2. **Copy** the **Application ID** and **object ID.** The application ID value is referred as the **client ID.**
3. **Note down** the Copied **Application ID** and **object ID** which is highlighted in the below figure, this will be used while deploying the **ARM template.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d8.png)

### Task 2: Create Session ID

1.	Use the below **URL to generate GUID.**

<https://www.guidgenerator.com/>

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d9.png)

2. Click **Generate some GUIDs!** This will generate **GUID** in Results box. 
    
3.	**Copy** and **Note down** the generated GUID which is highlighted in the below figure, this will be used while deploying the **ARM template.**  

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d10.png)

### Task 3: Deploy ARM Template

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

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d13.png)
    
**To deploy a template for Azure Resource Manager, follow the below steps.**
1.	Go to **Azure portal.**
2.	Navigate to **Create a resource (+)**, search for **Template deployment.**
3.	Click **Create** button and click **Build your own Template in the editor** as shown in the following figure.
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d13-1.PNG)
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d13-2.PNG)
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d14.png)

4.	The **Edit template** page is displayed as shown in the following figure.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d15.png) 

5.	**Replace / paste** the template and click **Save** button.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d16.png)

6. The **Custom deployment** page is displayed as shown in the following figure. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d17.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d18.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d19.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d20.png)

####   Inputs

These parameter values enable you to customize the deployment by providing values. These parameters allow to choose the solution type, region and AD Application details. 

**Parameters for Basic Solution:**

If you want to deploy the **Basic Solution** you must enter the values for the parameters mentioned in the **Exercise 1, Task 3**.

For **basic solution,** enter the parameters as shown below. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/1.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/2.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/3.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/4.PNG)

**Parameters for Standard Solution**

If you want to deploy the **standard solution** you must enter the below parameters as shown in the screens.

For **standard solution,** select new values for **numBlockMakers as 2, apiManagement as YES/NO** and keep the default values for other parameters. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/5.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/6.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/7.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/8.PNG)

**Parameters for Premium solution:**

If you want to deploy the **Premium solution** you must enter the below parameters as shown in the screens.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/9.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/10.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/11.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/12.PNG)

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

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d33.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d34.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d35.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d36.png)

#####   Outputs
Go to **Resource Group** -> Click **Deployments** then click on **Microsoft.Template** after that click on **Outputs**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d37.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d38.png)

**Result:** After completing this exercise, you should have successfully created and configured an Azure web app to support WordPress blogs.

## Exercise 2: Configure Secure Cold Chain Solution to a working state

**Scenario**

This exercise explains about how to configure the Secure Cold Chain solution to a working state. It covers all the post deployment steps and the device configuration steps.

The main tasks for this exercise are as follows:

1.	Deploying smart contract and getting the Contract Address.

2.	Performing Azure Site Recovery for Block Chain Virtual Machines.

3.	Importing Function App into the API Management.

4.  Building the Web App code.

5.  Connecting Devices to the solution.

6.  Device Configuration.

### Task 1: Deploying smart contract and getting the Contract Address.

Associating **NAT rule** of port **8545** to the **BM0 Machine**

1. Click on **Load Balancer** resource and click on **Inbound NAT rules** in left side.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de10.PNG)

2. Click on **NatBM0_RPC_Port** rules

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de11.PNG)

3. Click on Dropdown **Target virtual machine** to **BMO** and **Network IP configuration** to **BM0** and click **Save**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de12.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de13.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de14.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de15.PNG)

1.	Go back to the **Load Balancer** and copy IP Address and port: **3000** paste it in to the putty.

**NOTE**: If deployment type is **Standard (OR) Premium** you have to use **Blockchain traffic manager URL** along with port **3000** to SSH into the **BM0 VM**.
    
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d51.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d52.png)
    
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d53.png)    
    
Click **Yes** to continue.    
    
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d54.png)    
    
Login ID: **gethadmin**

Password: **Password@1234**
    
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d55.png)    
    
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d56.png)  

1.	Run the following command in **BM0** to download the **script(smart-script.sh)** to deploy the smart contract

$wget https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/scripts/smart-script.sh

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d57.png)

2.	Run the following command to change the permissions of the file **smart-script.sh**

$ sudo chmod 777 smart-script.sh 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d58.png)    
    
3.	Run the script by using below command 

$ ./smart-script.sh http://52.247.204.66:8545 https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/scripts/contract.sol https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/scripts/smart_contratct.js

NOTE: The IP address used in the RPC URL will change for every deployment. So use the updated IP address to use in RPC URL. The IP address for forming RPC URL is taken from the LoadBalancer IP address if the solution type is Basic. If the solution type Standard (OR) Premium you need to use the Blockchain Traffic Manager URL  

Rpc Url: $1
Contractsol: $2
smart_contract_js: $3
    
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d59.png)    
    
4. Contract address displayed on the screen, make a note of the contract address for future reference.   
    
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d60.png)

####    Running Blockchain servic in TMT-VM

After the contract deployment you have to perform the following steps to run the block chain cron job service in tmt-vm.

For that you have to provide the following values from the output section of the ARM and provide it to the following script url.

Refer output section from the ARM deployment **4.2.1**

1. Blockchain IP or FQDN: :**"2.175.243.187"** (or you can provide the RPC URL with FQDN as well **ex**: test1htih.westus2.cloudapp.azure.com)

2. Password : **"Password@1234"** (ethereumAccountPsswd)

3. ContractAddress : **"0xd761de896114f745e5ef789532523ff9ab3cf553"**

4. Gas Limit: 40000000

5. Login into the **TMT-VM** using **Putty**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d60-1.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d60-3.PNG)

Login ID: **gethadmin**

Password: **Password@1234**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d60-5.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d60-6.PNG)


6. Run the following command: 

    **wget "https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/scripts/blockchain-service.sh"**

    **cat blockchain-service.sh | tr -d '\r' > blockchain-service.sh1 | mv blockchain-service.sh1 blockchain-service.sh**

    **sudo chmod 777 blockchain-service.sh**

    ./blockchain-service.sh &lt;Blockchain IP&gt; &lt;Password&gt; &lt;contractAddress&gt; &lt;Gas Limit&gt;

**Ex**: ./blockchain-service.sh "52.175.243.187" "Password@1234" "0xd761de896114f745e5ef789532523ff9ab3cf553" "4000000"

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d60-7.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d60-8.PNG)

### Task 2: Performing Azure Site Recovery for Block Chain Virtual Machines.

**Note: This step is performed only for the Standard and Premium Solution deployments.**
1.	In Azure portal search for “site recovery”  as shown below and click on **Recovery Services Vaults.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr1.png)

2.	Click on + **Add**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr2.png)

3.	Enter the required details and click on **Create**. 
Select **Location**(East US2) value which is different from the resources Location(Blockchain VMs ).
**Note:** In this case, Blockchain VMs are deployed in West US2 so you can choose Location as East US2

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr3.png)

4.	Click on the **Resource Group(cc-standard-asr)** which have created above , then click on the **site recovey vault(cc-standard-vault)** you have created above. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr4.png)

5.	Click on **Site Receovery** and then click on **Prepare Infrastructure**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr5.png)

6.	Click on **OK**  after selecting the values as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr6.png)

7.	Click on **Ok** 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr7.png)

8.	Click on **Step1: Replicate Application**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr8.png)

9.	Enter the required details as shown below and click on **OK.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr9.png)

10.	Select the virtual machine which you want to replicate, in this case you need to select Blockchain VMs Only and click on **OK**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr10.png)

11.	In the next screen keep all the values to default and then click **Create tagrget resources.**

**NOTE:** If you want,  you can customize the values by clikcing the Customize link

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr11.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr12.png)

12.	Click on **Enable Replication.** It will create the required resources as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr13.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr14.png)

13.	Click on the **Resource Group(cc-standard-asr)** which you have created as part of ASR as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr15.png)

14.	Click on the **Site Recovery Vault(cc-standard-vault)** which you have created before

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr16.png)

15.	Click on **Replicated Items**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr17.png)

16.	Once you click on Replicated Items, it will show all the replicated VMs. If the Status is “**Protected**” then you can do Failover/ Test Failover otherwise you need to wait until the status becomes “**Protected**”.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr18.png)

**NOTE:**  The Failover steps can be performed once the primary region fails as discussed in **Admin Guide in section 5.1.2.1**

### Task 3: Importing Function App into the API Management

If the option for the parameter **apiManagement** is **YES**, then you must perform the below steps to import the all the functions(operations) of a **function app** into the **API Management**. 

1. Go to **resource group** [Symbol] select **API Management.** 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api1.PNG)

2. Select **API’s** under **API Management** in the left-hand side.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api2.PNG)

3. Click on the **API** which is named as like function app name.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api3.PNG)

4. Click on the … icon to import the function app.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-oldChain/master/Documentation/images/api4.PNG)

5. Click on **browse tab** to select the function app that we want to import.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api5.PNG)

6. Now click on **configure required settings** to choose your function app.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api6.PNG)

7. Now choose the **function app** of your resource group and click on **select**. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api7.PNG)

8. After few seconds **all the operations of the function app** will load and then click on **select.** 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api9.PNG)

9. Click on **Import.** 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api10.PNG)

10. After some time all the operations in a function app will load into the API Management. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api11.PNG)

11. Now click on **products** under API Management in the left-hand side and then click on starter.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api12.PNG)

12. Click on **settings** and then **uncheck** the **required subscription** option then **save**. 

Follow the below screens to uncheck the required subscription option. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api13.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api14.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api15.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/api16.PNG)

### Task 4: Building the Web App code.

Follow the below steps to build web application UI code to point to the deployed resources 

1.	Open the **ProjectTitanUICode** from **UI WebApp** folder from the **ColdChain** folder. 

 **Note:** Clone the cold-chain repository to your local system and perform the below steps

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d61.png)

2. Open the **src** folder from **ProjectTitanUICode** folder.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d62.png)

3.	Open environment folder and update the values of **environment.prod** file.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d63.png)

4.	Update the values **API_Endpoint, SAS_Token,blobAccessUrl,storageUrl, client_id,web3_password,contractAddress,HttpProvider,gasLimit and BingApiKey**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d64.png)

5. You can take all the resource values from the ARM template output section                                         
                                           
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d128.png) 

6.	You can get all the values from the Azure portal as shown below and use the same contract address which you have copied in the earlier step (**5.1. Deploying smart contract and getting the Contract Address**)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d65.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d66.png)

7.Click on **Storage Account -> Shared access signature.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d67.png)

8. Click on **Generate SAS and connection string** button. Copy the **SAS token** and **Blob Access URL** and update into **environment.prod.ts** file.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d68.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d69.png)

**Create Bing Map API**

1.	In Azure portal click on Create a resource.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/b1.png)

2.	Search for “bing maps” as show below and click on Bing Maps API for Enterprise.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/b2.png)

3.	Click on Create.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/b3.png)

4.	Fill all the required details as shown below and click on Create.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/b4.png)

5.	Go the resource group and Click on Bing map resource 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/b5.png)

6.	Click on the Key Management and copy the masterkey this value you need to use for BingApiKey

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/b6.png)

 Here you can updated the details:
 
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d70.png)

**NOTE1**: If you choose api Managemnet option as **YES** for the deployment then you have to provide the api management test url under the API_Endpoint of the environment.prod.ts file.

**NOTE2**:If you chosse deployment type as **standarad(or)premium** with api MAnagemnt as NO option then you have to provide the below URL's under the following variables.

1.API_Endpoint : <"http://cctrafficmng-fun4ji7q.trafficmanager.net">

2.HttpProvider: <"http://cctrafficmng-bc4ji7q.trafficmanager.net:8545">

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d127.png)

9. After updating the **environment.prod.ts** click on open **Node.js command prompt** window and go to the ProjectTitanUICode location i.e. you web application code location as shown in the following screenshots.

**NOTE:** make sure that you have latest **node modules installed** and you have **Angular CLI** installed on your local machine

Command: **npm install -g @angular/cli**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d71.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d72.png)

10. Here we can **install npm**

Command: **npm install**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d73.png)

11.	Run the following command to build the code 

Command: **ng build –prod**

Note: Before running the above command make sure that you have installed Angular CLI.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d74.png)

12. After successful build, you will get the folder called **dist**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d75.png)

13.	Open **AngularFrontEnd** from the **dist folder,** add the web.config(download it from here ) to the **AngularFrontEnd** and select all the files then zip them. 

**Note**: Download the Web.config file from the repository

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d76.png)

14.	Open kudu tool to upload the built web application code to the web app. You can open the Kudu tool by adding the scm in the web App URL as shown below 

Ex: <https://webapikowgh.scm.azurewebsites.net)>

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d77.png)

15.	Click on **Tools** dropdown list and click **Zip Push Deploy** to push the zipped web app code as shown below.

**Note:** Remove the existing files before you push new code. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d78.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d79.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d80.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d81.png)


### Task 5: Connecting Devices to the solution

#### 5.1. TMT-250 Device Configuration

To setup the Teltanica TMT-250 device follow the steps mentioned below.

**Inserting micro SIM card and connecting the battery to TMT250**

1.	Unscrew **4 screws** counter clockwise.
2.	Remove the **cover.**
3.	Insert **Micro-SIM** card as shown. Make sure that **Micro-SIM card cut-off corner** is pointing forward to slot.
4.	Connect the **battery** as shown to the device.
5.	Attach device cover back and screw in all **4 screws.**
6.	Device is **ready** to be used.

**PC Connection**

Connecting the **TMT-250 device** with your local system

Connect device to computer using **Magnetic USB cable** or **Blue-tooth** connection:

1.	Using **Magnetic USB cable**

    You will need to install USB drivers 
    Below is the link to download your TeltonikaCOMDriver.zip to install the USB driver.
    <https://teltonika.lt/downloads/en/fmb120/TeltonikaCOMDriver.zip>

2. Using **Blue-tooth**

    TMT250 Blue-tooth is enabled by default. Turn on **Blue-tooth** on your PC, then select **Add Blue-tooth or another device > Blue-      tooth.** Choose your device named – **“TMT250_last_7_imei_digits”,** without **LE** in the end. Enter default password **5555,**        press **Connect** and then select **Done.**

   Click on **Add Bluetooth** or another devices option to add the teltanika.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d82.png)

Click on **Bluetooth.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d83.png)

Choose your **teltanika device ID without LE.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d84.png)

Provide the Default **password** as 5555 and click on **connect.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d85.png)

After paired click on **Done.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d86.png)

3. You are now ready to use the device on your computer.

**Configurator**

Below is the link to download the latest TMT250 **Configurator** version.
<https://wiki.teltonika.lt/wiki/images/f/f5/FMB.Configurator_v0.16.1.17313_C.004.zip>

After downloading, Extract the .zip file and double click on the **configurator.exe** to open the TMT-250 Application.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d87.png)

Now the application will appear as below.

Click on the **Device icon** to connect the device.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d88.png)

After connection to Configurator **Status window** will be displayed

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d89.png)

After the application opens you can see the pop up of parameters loaded success.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d90.png)

Now go to **GPRS property** on the left-hand side and set the below properties.

**1.APN** (it should be cellular network) if it is AIRTEL then you need to provide the below APN. Based on the cellular you have provide specified domain.

**2.Domain:** Provide your TMT-VM **public IPAddress.**

**NOTE**: If the deployed solution type is **standard or Premium** you must provide the **traffic manager** DNS name under the Domain field.

**Ex: “cctrafficmng-tmtjct7q.trafficmanager.net”** 

**3.Port:** Set the port as **21684.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d91.png)

After providing all the details click on **save to device** tab on the top.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d92.png)

Go to **Status GSM Info**
Here you can see the full information like the **Number of records sent, SIM State, GPRS Status and Socket Information.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d93.png)

For more information regarding configuration of **TMT-250** please follow the below link.
https://wiki.teltonika.lt/view/TMT250_First_Start

####    Connecting Rigado

1.	Connect **LAN cable** to the **Rigado** and switch on it.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d94.png)

####    Connecting Beacons

1.  Switch on the **Beacons (Sensor)** and keep it within the range of **Rigado.**

    Note: If Beacon will show **Red light,** it is in **ON** state otherwise **OFF** state

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d95.png)

Press **ON** the **beacon 3 times,** at that time if it shows **Red light,** it is in **ON** state otherwise it shows **Green light,** it is in **OFF** state.

### Task 6: Device Configuration

####    Build and Deploy Snap to Gateway

Below listed are the steps to be followed to build and deploy snap to Rigado Cascade-500 IoT Gateway.

**a. Development Host** - This computer or virtual machine should have Ubuntu 16.04 LTS and will be used to edit source files, test scripts, and interact with the snapcraft CLI. It may have any architecture (amd64, x86, etc). This device must have an HCI0 interface with BLE enabled.

**b. Build Host** - NodeJS snaps are not cross-compilable, so this build computer must have an armhf processor architecture and have enough resources to build the snap. The Raspberry Pi 3 is recommended because it has the armhf architecture, and can run the Ubuntu Core OS (which simplifies the build process). 

**I. Setting up the Development Host**

1.	Install Node.js (>=6.11.4).

2.	Install required libraries with the following command:

    **$ sudo apt update**

    **$ sudo apt-get install bluetooth bluez libbluetooth-dev libudev-dev g++ python2.7 git build-essential curl libssl-dev npm**

3.	Download the project (codebase of Gateway) to your development host and navigate to the project and enter the following command:

    **$ npm install**

4.	This will install all the dependencies which are required for the project mentioned in package.json file.

##### 6.1.1. Snap Building

1.	For now, the Node.js plugin for snapcraft doesn’t support a cross-platform build. Raspberry Pi is required for building the snap. For installation of Raspberry Pi follow the steps mentioned in the link <https://docs.rigado.com/en/latest/creating-apps/prereqs.html#developer-prereqs-rpi.>

2. Once Raspberry Pi is set up, login by using the following command:

$ ssh abc@175.21.10.9 [IP address of the RaspberryPi]

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d97.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d98.png)

3. Copy the project folder from your local to Raspberry Pi

   **$ scp -r user@175.21.10.4:/home/user/Project-Titan/.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d99.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d100.png)

4. Install Classic

   **$ sudo snap install --beta --devmode classic**
   
5.	Once Classic is installed, switch to classic mode by entering the following command:

   **$ cd Gateway Source Code**
   
   **$ sudo classic**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d101.png)

6. In Classic mode, install snapcraft:

      **$ sudo apt update**
      
      **$ sudo apt install snapcraft build-essential git**
      
7.	Once snapcraft is installed [in classic mode] navigate to the project folder, where the snapcraft.yaml file is present, change the version number to the higher number than the one present in the file.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d102.png)

**NOTE:** if you’re building the snap multiple times make sure that the version should be updated to the next number in **snapcraft.yaml** file. Ex: If version is 1.9.10 make it as 1.9.11 for the next build.

8. You should change the **function App Url(API_endpoint)** and **IoT Hub connection string(IoT Hub name) url** in **Config.json** file for before building the snap.

**Note**: You can take the URL from the output section of ARM template.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d129.PNG)

**Note**: If the Deployment type is Standard or Premium, you have to provide Traffic Manager URL

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d96.png)

**Note**: If you want to re-build the snap you need to delete the following folders

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d96-1.png)

To build the snap, enter the following command

**$ sudo snapcraft**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d104.png)

9. Once the snap is built, it will create an abc_test_1.0.1_**armhf.snap** file. Copy this snap from the build host [i.e Raspberry Pi] to development host [i.e. Ubuntu 16.04 machine] using the following command:

**$ scp abc_test_1.0.1_armhf.snap** <user@175.21.10.4:/home/user/>

This will copy the snap to Local at the path mentioned.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d105.png)

####    Uploading the snap to Gateway

1.	Switch to Development host and login to <https://app.rigado.com/.>

2.	Navigate to Apps page and click on create app and enter a unique name for the app and upload the snap as your first revision. 

    **Create new App**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d106.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d107.png)

Application created successfully

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d108.png)

Create Bundle for the specific Application.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d109.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d110.png)

Bundle created successfully and add tag to that bundle

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d111.png)

Select an App and add app to that Bundle then save it.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d112.png)

Navigate to created App and upload the Snap by following the below steps.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d113.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d114.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d115.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d116.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d117.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d118.png)

**Note: The name of the app must be same as the name mentioned in snapcraft.yaml of the project**

3.	When it’s done uploading, a modal will ask you if you want to release the app revision to a channel. Select the edge channel and click the RELEASE button.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d119.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d120.png)

####    Verifying the device configurations

1.	Go to **Azure Portal.**
2.	Click on the **Resource Group** and Navigate to the **IoT Hub resource**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d121.png)

3.	Click on the **IoT Hub** and Navigate to the **IoT Hub Overview**, here you can see the **IoT Hub Message count.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d122.png)

1. Click on the **IoT devices** in **IoT Hub,** here you can see the **Gateway Device Id.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d123.png)

5. Click on the **Gateway**  

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d124.png)

6. Click on the **Device twin**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d125.png)

7.	Once all the above configurations are correct you can see the device status as connected as shown below

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d126.png)

## Exercise 3: Use the Secure Cold Chian Solution

**Scenario**

This exercise explains about how to use the Secure Cold Chain solution.

The main tasks for this exercise are as follows:

1.	Accessing the Web Application.

2.	User Management.

3.	Device Management.

4.  Shipment Management.

### Task 1: Accessing the Web Application

Once the solution is deployed successfully, navigate to the Resource Group and select the created resource group to view the list of resources that are created in the Resource Group as shown in the following figure.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u1.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u2.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u3.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u4.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u5.png)

1.	Go to **Resource Group** -> Click on **Web App** from the below resources.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u6.png)

2. Copy the **Web App URL** and open it in the browser.

**Note**: If it is Standard or Premium, you need to copy the **Traffic Manager URL(websiteURLHA)** and open it

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u7.png)

3. Before entering the Web App URL, you can remove the **https**. Please enter <http://webapigw6ej.azurewebsites.net> you will be redirected to Azure AD Authentication page.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u8.png)

4.	Enter Azure AD Authorized User Credentials.

   User ID: *******@SecureColdChain.com**
 
   Password: ******************
 
After successful validation by the Azure AD, based on the user role the web app will redirect you to Admin Page if the user role is Admin, else it will redirect to Dashboard page hiding the Admin Tab for anyone to access.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u9.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u10.png)

5.	The administrator will have full access to the system. Below mentioned are the main roles for an administrator. 
    * User Management
    * Device management 
    * Shipment Management

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u11.png)

### Task 2: User Management

1.	Click on the User Management tab to create users. In user management admin can perform following actions.
     * Adding User 
     * Editing/Updating User 
     *	Deleting User

####  Adding of User and assigning role

1.	Click on the **user** tab to create users.
  
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u12.png)

2.	In right side of the user management page click **+** to create a user. When you click on the **+** symbol, a pop up will open which looks like the image shown below: 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u13.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u14.png)

3.	Click on Full Username, list of all the user who are included in the Active Directory Group, the **Email** field gets auto populated and you assign the role by clicking in the **Role** field where in you can select any role from the drop-down list and assign it to the user by clicking on the **Save** Button.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u15.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u16.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u17.png)

4.	After saving the User Management tab, you will get a pop-up window **Added User** and the user will be seen in the list of active users.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u18.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u19.png)

####  Editing or Updating User Role

1.	When you click on the **role** column against any user, you will be able to see a drop-down list consisting of different roles as seen in the below image.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u20.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u21.png)

2.	After selecting the role from the list, you need to click on **right green** button seen in the last column of the table. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u22.png)

3.	The user role will be updated, and you will get a response as under.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u23.png)

4.	You can now check the **user role** against the user in the active user list which will be changed to the new role that you have assigned.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u24.png)

#### Deleting a User

1.	Click on **delete symbol** as seen in the last column of the table.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u25.png)

2.	You will get a response as below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u26.png)

3.	The user will be removed from the active user’s list table as seen below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u27.png)

### Task 3: Device Management

####  Gateway and Tracker Onboarding

 1.	In **Device Management** tab, the user to on-board **gateways** and **trackers** on to the system by clicking in the **+ Add Device** Button in right side of the page

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u28.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u29.png)

2.	After clicking on that **Add Device** button a popup box will open asking you to add **Mac ID** and select the type of **Device** from a drop-down list. Once you have filled the required information, click on the **Add button** which will store the device information in the database.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u30.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u31.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u32.png)

3.	Once the device type like **Gateway** and **Tracker** is successfully added to the database, you will get a popup window to response as below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u33.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u34.png)

4.	Here you can see the **added Gateway** and **Tracker**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u35.png)

####  Off boarding or Removing Onboarded Gateway and Tracker

1.	Click on **Remove** icon to remove the corresponding device you want to off-board.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u36.png)

2.	Once you click on the **delete device button** highlighted in the image above, you will get a response as below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u37.png)

3.	The Gateway with Mac-Id **C031061830-00527** will now be removed from the **Onboarded device** list as below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u38.png)

### Task 4: Shipment Management

The web application allows the admin to create and manage the shipments. The web application will allow the admin to map the beacons with product, box, carton and pallet that will be used during the transport. After that, the web application will allow the admin to create association between objects which will help while monitoring the sensor data during the transport.  After the association among the objects is created, the admin will have assign gateways and trackers to each pallet. Each of this process will be discussed in this section.

####  Create Shipment

1.	Click on **Shipment tab** under **Admin page**, here you can **create a shipment** and **Associate**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u39.png)

2.	To create a new **Shipment**, you need to click on the + on the top right corner above the **shipment List**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u40.png)

3.	Once you click on the **+ symbol**, a popup box opens for you to add the required information about the shipment such as **Shipment ID, Purchase Order, Logistics Partner, Source, Destination** and **list of products**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u41.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u42.png)

4.	Once you click on **Create button** you will get a popup window **Consignment successfully** added to **Blockchain**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u43.png)

5.	Once you **created shipment**, click on **refresh** symbol and you can see the **added shipment**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u44.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u45.png)

**Note**: The next step is to **Map Beacons** to the **object** and assigning **Tracker** and **Gateway** to each of the **pallets** present in the **shipment**.

####    Mapping Beacons to Objects

The web application provides an interface for the admin to map each beacon sensor with an object (ex. Product, Box, Carton, Pallet). These mapping data is required to monitor the sensor data during the transit of the shipment. This mapping will help in monitoring the sensor data at multiple level (Product level, Box Level, Carton Level and Pallet Level).

1.	In the **Shipment** tab click on the **Associate** button shipment.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u46.png)

####    Adding a Mapping

1.	You can see a **green Map button** on the top left corner above the table and a drop-down list below it in the above image. Click on **Map button** you see a new row is added in the table where minimum and maximum threshold values will be automatically populated based on the storage class you have selected. These values are also editable.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u47.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u48.png)

2.	To map a beacon to an object, you need to add the **Beacon Id** of the **Beacon Sensor**, the **Object ID** of the object you want to map the beacon, the type of the Object and the **Content** of the object as below
3.	Once you have filled all the related information, click on the **right green symbol** in the table. This will save the mapping information in the database.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u49.png)

4.	It will open the popup window to add the database.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u50.png)

5.	We have added multiple **Beacons** to the database as shown in below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u51.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u52.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u53.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u54.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u55.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u56.png)

####    Create Association among Objects

Once the beacons are mapped with the object, the next step is to create association among the objects. This association will help us in defining hierarchy among the objects in a shipment.

1.	Once you have clicked on the **Next button** after mapping your beacons and objects.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u57.png)

2.	Simply **drag** and **drop** the labels from the **left section** to **right section** of the page. This definition of hierarchy is needed to know till which level we are monitoring the sensor data.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u58.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u59.png)

3.	After defining the hierarchy, click on the **Next button** to **Associate objects**. The following page will appear.

4.	We have the 4-level of hierarchy **Box -> Product.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u60.png)

5.	You need to add **object id** of **box against** the box field and **product against** of the **product** in the product field and **press enter**. This will add the product id in the below text area in the form of a label as seen below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u61.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u62.png)

6.	Once you have added **product id** and **box id**, click on the **Associate button**. This will save the association in database

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u63.png)

7.	You will be able to see this association under the **Association** section of the page.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u64.png)

8.	You can add **multiple Products** this way.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u65.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u66.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u67.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u68.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u69.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u70.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u71.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u72.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u73.png)

6.	You will be able to see an **association summary** as below. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u74.png)

####    Assigning Gateways and Tracker

Click on the **+ button** on the top right corner, a row will get added where you need to enter **Pallet’s Object ID, Gateway's** and **Tracker’s** serial numbers and click on **create** button.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u75.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u76.png)

After the **Gateway** and **Tracker** is successfully assigned to the **Pallet**, you will see a response like **Gateway is assigned**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u77.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u78.png)

Here you can see the added number of **gateways, trackers** and **beacons.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u79.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u80.png)

####    Uploading and Viewing Documents

#####   Uploading Documents

Click on **document icon** in the **shipment tab**, it will expand a section where you can upload your **documents**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u81.png)

Click on **Choose Files Button** which will open a window for you to select the file.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u82.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u83.png)

Once the file is uploaded, you will see **File Uploaded Successfully** message as below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u84.png)

The next step is to upload document information to the **Blockchain**. For this, select the **Document Type** from the drop-down list.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u85.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u86.png)

Click on **Upload to Blockchain** button which will upload the document information in the **Blockchain**. After successful uploaded, you will see a response as below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u87.png)

#####   Viewing Documents

When you click the V**iew Document Button**, a section gets expanded below the ribbon where you will be able to see a table which contains a list of documents against the respective shipment. The expanded section is **highlighted** in the below image.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u88.png)

When you click on **View icon** button you will be able to view the document in the new tab or it will get downloaded if the file extension is other than **.pdf**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u89.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u90.png)

#####   Updating Shipment Status

1.	Click on **Update Status** button, a dialog box will open as below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u91.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u92.png)

2.	From the drop-down list, select the status of your choice as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u93.png)

3.	After you have selected shipment status, click on the **Update Status** button. This will update the status value of the shipment in the database and a record of this update will be stored in the **Blockchain**. After successful uploaded of the status, you will get the following response from Blockchain.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u94.png)

4.	To check if the status of the shipment is updated or not, click on **shipment ID** of the ribbon as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u95.png)

5.	This will open the dashboard of that respective shipment where you can check the status value under **Shipping Details Sections** as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u96.png)

6.	To check whether **the record of shipment status is recorded in Blockchain or not**, you can simply check the **Blockchain Transactions** sections under the **Shipping Details** sections where all the transaction made to the Blockchain are shown in chronological order.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u97.png)

7.	Click on the transaction hash which will show the **Transaction details** in a modal as below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u98.png)

####    Deactivating Shipment

1.	To **deactivate/close** any shipment, click on **Close button** which is highlighted in the below image. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u99.png)

2.	After clicking on the **close button**, a modal will open as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u100.png)

3.	From the drop-down list, select the type of status you want to **close/deactivate** the shipment with.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u101.png)

4.	Once you have selected the **closed**, click on the **Deactivate Shipment** button. A dialog box will open which will ask for confirmation about **closing/deactivating** the shipment as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u102.png)

5.	When you click on **Yes button**, you will get a response from **Blockchain** as below and the shipment is now **deactivated.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u103.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u104.png)

6.	When you reload your **Shipments Tab**, the shipment will get **deactivated** and the shipment will be represented by a dark red ribbon as shown in the below image.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u105.png)

####    Dashboard

#####   Dashboard Summary

Click on **dashboard tab** it will navigate the dashboard page.

1.	In **Current Shipment Section**, when you click on **Shipment ID**, marker on the map will be highlighted that shows the location of that shipment.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u106.png)

2.	When you **click** on that marker, an overlay popup will be displayed against the marker that will show the **Shipment Details** of that **Shipment**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u107.png)

3.	 In the **Current Shipments Section,** when you click on the **i  symbol** against a particular Shipment ID, an accordion will be displayed below the S**hipment ID** which will show an overview of the shipment status 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u108.png)

#####   Specific Shipment Dashboard

When you click on **eye symbol** against a **Shipment ID** in **Current Shipment** section it will redirect you to a page that will have details of the **Shipment**. This page has **7 tabs** which will be described in this section. The five tabs are: **Tracker, Status, Devices, Incidents, Blockchain Alerts Stored Sensor Data and Stored Sensor Alerts**. The main layout of this page consists of **Shipment Details, Alert Summary Tabs, Blockchain Transaction, Shipping Object Details** and Tabs Section.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u109.png)

#####   Shipping Details Section

This section shows basic information about the shipment such as **Shipment ID, Purchase Order Number, Source, Destination and Status** of the shipment and the last known time of **GPS signal.** This section is highlighted in the below image.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u110.png)

**Blockchain Transactions Section**

This section consists history of all the **Blockchain Transactions** in chronological order. The type of transaction is also shown below the timestamp. This section is highlighted in the below image.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u111.png)

When you click on the **Transaction Hash**, a dialog box will open which will show the **Transaction Details** as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u112.png)

**Shipping Objects Section**

This section consists of number of **Pallet, Carton, Boxes** and **Products** that are packaged under a **specific shipment.** This section is highlighted in the below image.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u113.png)

#####   Tracker Tab

The **Tracker Tab** will be rendered which will show the last known location of the **shipment.** The view of this tab is shown above. When you click on the marker, a pop-up will be display next to the marker that will show **shipment details** and **incidents.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u114.png)

#####   Status Tab

The Status Tab will show a list of objects along with their **Object ID, Beacon ID**, the object it is associated with, **Temperature, Humidity, Shock** and **Vibration Alerts,** and count of incidents.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u115.png)

User can visualize the **Temperature** and **Humidity** data of each object through a chart that will be rendered when a user clicks on **icon button.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u116.png)

You can select the date range by clicking in the box area where it says **Click her to change Date Range**. After clicking, you will get date selector as below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u117.png)

You can select the date range and click on **update button**. The graph will get updated by the **temperature** or **humidity** values that falls under the selected date range.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u118.png)

#####   Devices Tab

The **Devices Tab** will consist of a list of association of **beacons** and **objects** with **Gateways.** The connectivity status of the devices will also be shown in this list.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u119.png)

#####   Incidents Tab

The **Incidents Tab** consists of a list of all the alerts that has occurred over the course of monitoring the shipment. The list contains details about the alerts like the object **(Product, Box, Carton or Pallet)** where the alert has occurred, **timestamp** when the alert has occurred, type of alert **(Temperature, Humidity, Tamper, Shock/Vibration Alert)** and the location where the alert has taken place. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u120.png)

One can acknowledge the alert by clicking on the **Acknowledge** button. Clicking on that button will open a dialog box asking for acknowledgement note. Once you fill the acknowledgement note, click on **Acknowledge** button to store this note in the database.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u121.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u122.png)

The incident which is already acknowledged will be marked as **Acknowledged** under **Action** column. You can view the Acknowledgement note by clicking on the button. This will open a dialog box which will show the Acknowledgement Note as below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u123.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u124.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u125.png)

#####   Blockchain Alert Tab
This tab shows all the alerts that are stored in **Blockchain.** All the information regarding the alert will be shown in this tab along with **Alert Starting Time** and **Alert Ending Time.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u126.png)

#####   Stored Sensor Data

Here we can see the whatever we added Beacons and Sensor data.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u127.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u128.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u129.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u130.png)

#####   Stored Sensor Alerts

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u131.png)

#####   Report

 Click on the **View Report button,** the report corresponding to the selected **shipment** will be below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u132.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u133.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u134.png)

To download this **Report,** click on the **Download Report** button seen on the top left corner of the page.  

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/u135.png)

## Exercise 4: Administer the Secure Cold Chain Solution

**Scenario**

This exercise explains how to verify the data in resources, updating SKUs, enabling security steps for the resources and performing High Availabilty(HA) and Disater Recovery(DR) activities for Standard and Premium solutions.

The main tasks for this exercise are as follows:

1.	Security

2.	Monitoring.

3.	Hardening Components.

4.  Performing DR Strategies.

### Task 1: Security

####    Storage Security

#####   Secure Transfer Required

The **Secure transfer required** option enhances the security of your storage account by only allowing requests to the account from secure connections. For example, when you're calling REST APIs to access your storage account, you must connect by using HTTPS. "Secure transfer required" rejects requests that use HTTP.

In storage account overview click on configuration enabled the secure transfer required and click on save. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A01.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A02.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A03.png)

#####   Advanced Threat Protection

Azure Storage Advanced Threat Protection detects anomalies in account activity and notifies you of potentially harmful attempts to access your account. This layer of protection allows you to address threats without the need to be a security expert or manage security monitoring systems. 

In storage account overview click on advanced treat protection select on and click on save. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A04.png)

#####   Shared Access Key

A shared access signature provides delegated access to resources in your storage account. With a SAS, you can grant clients access to resources in your storage account, without sharing your account keys. This is the key point of using shared access signatures in your applications--a SAS is a secure way to share your storage resources without compromising your account keys.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A05.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A06.png)

#####   Encryption

One way that the Azure storage platform protects your data is via Storage Service Encryption (SSE), which encrypts your data when writing it to storage, and decrypts your data when retrieving it. The encryption and decryption is automatic, transparent, and uses 256-bit AES encryption, one of the strongest block ciphers available. 

On the Settings blade for the storage account, click Encryption. Select the Use your own key option.

You can specify your key either as a URI, or by selecting the key from a key vault. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A07.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A08.png)

* Choose the Select from Key Vault option.

* Choose the key vault containing the key you want to use. 

* Choose the key from the key vault. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A09.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A010.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A011.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A012.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A013.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A014.png)


####    SQL Database Security

#####   Advanced data security

Advanced data security (ADS) provides a set of advanced SQL security capabilities, including data discovery & classification, vulnerability assessment, and threat detection.

**vulnerability assessment**

* It helps to Assess, track, and improve the security of SQL databases, in Azure and on-prem.

**Configure vulnerability assessment:**

1.	Click on the Advanced Security and to enable ADS for all databases on the database server or managed instance, click **Enable Advanced Data Security on the server.**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A015.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A016.png)

2.	Click on the Vulnerability Assessment

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A017.png)

3.	To start using vulnerability assessment, you need to configure a storage account where scan results are saved. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A018.png)

4.	Select or create a storage account for saving scan results. You can also turn on periodic recurring scans to configure vulnerability assessment to run automatic scans once per week. A scan result summary is sent to the email address(es) you provide.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A019.png)

5.	Threat protection provides a new layer of security, which enables customers to detect and respond to potential threats as they occur by providing security alerts on anomalous activities.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A020.png)

If we configured vulnerability assessment and Threat protection, now we can go and check Scan.

**Click on the Scan and View the report**

  * The report presents an overview of your security state: how many issues were found and their respective severities. Results include warnings on deviations from best practices and a snapshot of your security-related settings, such as database principals and roles and their associated permissions.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A021.png)

Analyze the results and resolve issues

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A022.png)

**Set your baseline**

Once you have established your baseline security state, VA only reports on deviations from the baseline and you can focus your attention on the relevant issues.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A023.png)

#####    Azure SQL Database data discovery & classification

* Discovering and classifying your most sensitive data (business, financial, healthcare, personally identifiable data.

* The Overview tab includes a summary of the current classification state of the database, including a detailed list of all classified columns, which you can also filter to view only specific schema parts, information types and labels. If you haven’t yet classified any columns.

1.	Navigate to Advanced Data Security under the Security heading in your Azure SQL Database pane. Click to enable advanced data security, and then click on the Data discovery & classification (preview) card.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A024.png)

2.	The **Overview tab** includes a summary of the current classification state of the database, including a detailed list of all classified columns, which you can also filter to view only specific schema parts, information types and labels.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A025.png)

3.	To begin classifying your data, click on the **Classification tab** at the top of the window.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A026.png)

4.	You can also **manually classify** columns as an alternative, or in addition, to the recommendation-based classification:

* Click on **Add classification** in the top menu of the window. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A027.png)

#####   Auditing

Audit logs helps monitor data and keep track of potential security breaches or internal misuses of information. 

**Set up auditing for your database**

1.	Navigate to **Auditing** under the Security heading in your SQL database/server pane.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A028.png)

2.	Switch auditing ON and You now have multiple options for configuring where audit logs will be written.

*	You now have multiple options for configuring where audit logs will be written. You can write logs to an Azure storage account, to a Log Analytics workspace for consumption by Log Analytics, or to event hub for consumption using event hub. You can configure any combination of these options, and audit logs will be written to each.
If you prefer to enable auditing on the Server level, switch **Auditing** to **OFF**.

   (Or)

If you prefer to enable auditing on the database level, switch **Auditing** to **ON**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A029.png)

3.	Fill all the details and click Save.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A030.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A031.png)

4.	Clicking on **Open in OMS** at the top of the **Audit records** page will open the Logs view in Log Analytics, where you can customize the time range and the search query.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A032.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A033.png)

#####   Transparent data encryption for SQL Database and Data Warehouse

*	Transparent data encryption (TDE) helps protect Azure SQL Database, Azure SQL Managed Instance, and Azure Data Warehouse against the threat of malicious activity.

*	It performs real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.

*	Transparent data encryption encrypts the storage of an entire database by using a symmetric key called the database encryption key.

*	This database encryption key is protected by the transparent data encryption protector.

*	The protector is either a service-managed certificate (service-managed transparent data encryption) or an asymmetric key stored in Azure Key Vault (Bring Your Own Key). 

1.	You turn transparent data encryption on and off on the database level. 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A034.png)

2.	You set the transparent data encryption master key, also known as the transparent data encryption protector, on the server level. 

*	To use transparent data encryption with Bring Your Own Key support and protect your databases with a key from Key Vault, open the transparent data encryption settings under your server.

#####   SQL Database dynamic data masking

Dynamic data masking helps prevent unauthorized access to sensitive data by enabling customers to designate how much of the sensitive data to reveal with minimal impact on the application layer. It’s a policy-based security feature that hides the sensitive data in the result set of a query over designated database fields, while the data in the database is not changed.

**Examples**

| **Masking Function**           | **Masking Logic**       
| -------------              | -------------                                                                                                                              
| **Credit card**       | Masking method, which exposes the last four digits of the designated fields and adds a constant string as a prefix in the form of a credit card.  XXXX-XXXX-XXXX-1234  
| **Email**            | Masking method, which exposes the first letter and replaces the domain with XXX.com using a constant string prefix in the form of an email address.   aXX@XXXX.com

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A035.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/A036.png)

### Task 2: Monitoring Component

####    Application Insights

1.	Go to **Azure Portal -> Resource Group -> Web App**

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a1.png)

2.	Here click on the **Application Insight**

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a2.png)

3.	Click on **Turn on site extension** for **Web App** and **Function App**

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a3.png)

4.	Select following in the **application insight** and click **Apply** button it will navigating to the popup window. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a4.png)

5.	Click **Yes**

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a5.png)

6.	Go to **Resource group** and click on **application insight**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a6.png)

**Performance**

7.	On **Overview** page, Summary details are displayed as shown in the following figure.
    
8.	Click **Performance** on the left side of the page as shown below. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a7.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a8.png)

9.	Click on **Dropdown list** and select **Request time** in the following screenshot.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a9.png)

10.	After click on that **Request time**, it will open a new tab with some default queries & chart for the same. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a10.png)

11.	Click on **Request** it will open a new tab with request and response operations. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a11.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a12.png)

12.	Click **Chart** icon it should be display default queries & chart. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a13.png)

13.	Click on **Failure** on the left side of the page as shown below.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a14.png)

14.	Click on **View in Analytics** and select any of the analytics. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a15.png)

15.	After click on **Request Count**, it will open a new tab with some default queries & chart

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a16.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a17.png)

**Metric preview**

16.	Then select **metric explorer** from the left menu. 

17.	Here you need to select the resource from the drop-down list, select the metric what you want to give and select the aggregation as per requirement. 

18.	Here we can see the graph after specifying our need. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a18.png)

**Application Map**

19.	Application Map helps you spot performance bottlenecks or failure hotspots across all components distributed application. 

20.	After click on **application map** you can see the screen like below. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a19.png)

21.	When you click on **ccfunapp07gm** it will open popup window in right side and click on **Investigate Performance** button. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a20.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a21.png)

22.	To check the **logs**, click on the chart of which you want to see the logs then you will get the logs of each request as shown in below figure.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a22.png)


**Live Metrics Stream**

23. Click on **Live Metric Stream** to view the incoming requests, outgoing requests, overall health and servers of web application and function app.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a23.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a24.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a25.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a26.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a27.png)

####    OMS Log Analytics 

1.	Open **Azure Portal -> Resource Group** -> Click the **OMS Workspace** in resource group to view OMS Overview Section. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a28.png)

2.	Click **Azure Resources** on left side menu to view available Azure Resources.  

3.	Select your **Subscription** and **Resource Group** name from the dropdown list. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a29.png)


4.	Click on **Logs** in the left side menu it will open log **search box**.

5.	Copy **Resource group name** and past it in the **search box** and we write the **Kusto query language** and click **Run** button, it should show the Resource group Telemetry data.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a30.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a31.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a32.png)

6.	Here you can check the **resource group** information is displayed below the page as shown in the following figure.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a33.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a34.png)
  

7.	Copy **IoT Hub resource group** name and paste it in the search box with **Kusto query language** and click **Run**. 

8.	Here you can see the **IoT hub resource Telemetry information** is displayed below the page as show in the following figure.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a35.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a36.png)

9.	Here you can see the **IoT hub resource information** is displayed below the page as show in the following figure.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a37.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a38.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a39.png)

10.	Copy **Cosmos DB** resource group name and paste it in the **search box** with **Kusto query language** and click **Run**. 

11.	Here you can see the **Cosmos DB resource Telemetry information** is displayed below the page as show in the following figure.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a40.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a41.png)

12.	Here you can see the **Cosmos DB resource information** is displayed below the page as show in the following figure.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a42.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a43.png)

13.	Copy **SQL DB resource group** name and paste it in the search box with **Kusto query language** and click **Run**.

14.	Here you can see the **SQL DB resource Telemetry information** is displayed below the page as show in the following figure.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a44.png)

15.	Here you can see the **SQL DB resource information** is displayed below the page as show in the following figure.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a45.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a46.png)

### Task 3: Hardening Components

####    Application HA

**Note:  The following steps applicable for the Premium Solutions**

1.	Go to **Resource Group** -> Click on **Web App**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a42.PNG)

2.	Click on **Stop button** to stop the web application.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a48.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a49.png)

3.	Go to **resource group** and click on **traffic manager** then you can see the primary web app is stopped.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a50.png)

4.	Copy the **traffic manager URL** and check the use case flow.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a51.png)

5.	Go back to the **resource group** and click on **Function App**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a52.PNG)

6.	In the overview page click on **Stop** the **Function App**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a53.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a54.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a55.png)

7.	Go to **Resource Group** -> Click on **Stream Analytics**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a56.PNG)

8.	Click on **Stop the Stream Analytics**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a57.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a58.png)

### Task 4: Performing DR Strategies

####    Standard Solution Type


In this scenario, there is again a primary and a secondary Azure region. All the traffic goes to the active deployment on the primary region. The secondary region is better prepared for disaster recovery because the database is running on both regions. 

Only the primary region has a deployed cloud service application. Both regions are synchronized with the contents of the database. When a disaster occurs, there are fewer activation requirements. You redeploy Azure resources in the secondary region.

Redeployment approach, you should have already stored the service packages. However, you don’t incur most of the overhead that database restore operation requires, because the database is ready and running.  This saves a significant amount of time, making this an affordable DR pattern.

Standard Solution requires redeployment of Azure resources in secondary region when the primary region is down.
When user chooses Standard Solution type below Azure resources will be deployed 

*	Web Apps

*	Function App 

*	Application insights

*	Azure Cosmos DB

*	IoT Hub

*	Storage Account 

*	Document DB

*	SQL Server

*	Log analytics

*	Azure Active Directory

*	Automation Account

*	Stream Analytics 

*	TMT-VM 

*	API Management

When Primary region is down, and user needs to redeploy Azure resources to new region. Once redeployment gets completed below resources will get deployed.

*	Web App

*	Function App

*	Stream Analytics

*	API Management

*	TMT-DR

*Refer **Exercise 2** for Standard Solution Deployment.


####    Accessing the web application

1.	Go to **Resource Group** -> Click on **Traffic Manager** from the below resources

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a59.PNG)

2.	Copy the **DNS name** and open it in browser.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a60.png)

3.	Now you can see the landing page of **Web Application**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a61.png)

After opening the web application, you can verify the application flow (use case) like Device Onboarding, Shipment Creation, Reports. Once you done verifying the flow perform the following DR strategies.

**Note:  The following steps are for Standard and Premium Solution**

####    Performing Failovers 

######  Performing ASR Blockchain Machines Failover

1.	You need to go to the resource group for **Site Recovery Vault** which you have created as part of “**Performing Azure Site Recovery (ASR) for Block Chain Virtual Machines (VMs)**” in **Excercise 2, Task 2**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr15.png)

2.	Click on the **Site Recovery Vault(cc-standard-vault)** which you have created before

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr16.png)

3.	Click on **Replicated** Items

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr17.png)

4.	Once you click on the **Replicated Items**, it will show all the replicated VMs. You can click on the each VM which you want to Failover once the status is “**Protected**”

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr18.png)

5.	Once the Source Region fails (to simulate this, you can stop the Blockchain VMs in the primary Region (OR) you can simply change the endpoint in the Blockchain Traffic Manager to point to the Secondary/failover region LoadBalancer Public IP), You need to do the Failover to bring up the replicated VMs by clicking the **Failover** as shown below after clicking each VM individually.

**Note**: 1. You need to perform this step for all the Replicated VMs. 

**Note**: 2. Before performing Failover, you can do a Test Failover to verify that everything is working or not.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr19.png)

**Note**: You will get a warning as shown below in case if you do Failover without performing Test Failover. You can select the check box and click on Ok.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr20.png)

6.	Choose the **default values** and click on **OK**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr21.png)

7.	Then “**Failover**” starts as shown below. It will take some time to perform the **Failover**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr22.png)

8.	Once the Failover completes you can see a new notification which says “**Successfully completed the operation**” as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr23.png)

9.	Go to the **resource group** with the post fix as “**asr**” as shown below. (as you choose the default values, a resource group will be created with the source resource group name ending with “-asr”).

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr24.png)

10.	You see a **new VM** is created in the **resource group** as **source VM** as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr25.png)

11.	Repeat the Failover step for all the VMs, you can see all VMs in the “-asr” resource group as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr26.png)


12.	Once the Failover completes, then deploy the template in the “-asr” resource group (**coldchain-standard-solution-asr**) from the following link which deploys the Load balancer and NSG for the Blockchain setup.

https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/nested/asr-temp.json

13.	In Azure portal go to **Template deployment-> Custom deployment-> Edit template** 

Copy the template from the above URL and paste in the Edit Template text box as shown below 

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr27.png)

14.	After filling all the details like Load Balancer Name, Dns Host Name, publicIPAddressName and Location. Click on **Purchase**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr28.png)

15.	Once the deployment is successful, go to the resource group and configure the **Backend pools** and **Inbound NAT rules** as shown below

16.	Click on the **LoadBalancerBackend1**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr29.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr30.png)

17.	Click on **Inbound NAT rules**, then click on **Natssh0**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr31.png)

18.	Then select the **Target virtual machine** and **Network IP configuration** then click on **Save**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr32.png)

19.	Repeat this for all the other Nat rules **Natssh1, Natssh2** and **Natssh3**

20.	After updating the NAT rules **SSH** to all the VMs and run the **start-private-blockchain.sh** script.
And run the following command in another session (right click on the top section of putty and select **Duplicate session** then enter the credentials)

**sudo geth attach ipc:/home/gethadmin/.ethereum/geth.ipc**

21.	Use load balancer IP with port 3000 to 3003 to **SSH** to all the four VMs and run the script as shown below

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr34.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr35.png)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr36.png)

As shown above **SSH** to all other machines and run the scripts mentioned above.

**Note**:  If you are not able login into the VMs with the credentials set for your VMs in the source resource group (primary region), you need to reset the credentials using the Azure portal as shown below.

22.	Go to the “-asr” resource group click on the VM and then scroll down under the Overview until you find **Reset password**, then click on the Reset password. Enter the username as “gethadmin”

23.	then enter the new password and confirm password then click on **Update** as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr33.png)

24.	After running the scripts in all four VMs you need to make the Blockchain setup is up running in the secondary location i.e in ASR setup use the Load Balancer IP and open the Blockchain admin site as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr37.png)

If you get the correct **Peer Count** and the **Latest Block Number**, then your Blockchain setup is up and running.

**NOTE:** Now you have the failover Blockchain setup is up and running, you need to update the endpoint in the Blockchain Traffic Manager which was pointing to the primary region Blockchain setup, to points to the failover/secondary region Blockchain setup.

25.	Go to the source resource group and click on the Blockchain **Traffic Manager**.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr38.png)

26.	Click on the **Endpoints** and the endpoint.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr39.png)

27.	It opens the configured the endpoint, click on **Delete** to delete the previous endpoint.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr40.png)

28.	 Click on **Endpoints** and click on **Add**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr41.png)

29.	Enter Azure Endpoint as **Type, Name** can be any meaning full string, “Public IP address” as **Target Resource type**, select the Load Balancer Public IP address which you have created in the “-asr” resource group as **Target Resource**, 1 as **Priority** as shown below and click on Ok.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr42.png)

30.	 You can find the newly added endpoint as shown below.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/asr43.png)

Now the Traffic Manager points to the secondary region Blockchain setup.

#####   IoT Hub manual failover

Follow the below steps for doing the **IoT Hub manual failover**.

1. Go to **Resource Group** -> Click on **IoT Hub**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a62.PNG)

2. Go to **Manual Failover** in the left side menu.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a63.png)

3. Click on **Initiate Failover**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a64.png)

4. It will open a new window in right side menu, enter **Alias name** and click **Ok** button.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a65.png)
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a66.png)

5. Here you can see the manual failover from **East US 2 to Central US** is in progress.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a67.png)
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a68.png)

6. Here you can see the failover IoT Hub to the **Secondary Location Central US**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a69.png)
    
#####   Cosmos DB Manual Failover

Follow the below steps for doing the **Cosmos DB manual failover**.

1. Go to **Resource Group** -> Click on **Cosmos DB** resource.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a70.png)

2. Click on **Replicate data globally** in the left side menu.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a71.png)

3. Click on **Manual Failover**

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a72.png)

4. It will open a new window and select the **read reasons**, click **check box** and click on **Ok** button.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a73.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a74.png)

5. After manual failover is done, you can see the write region as **Central US** and read regions as **East US 2**

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a75.png)
    
#####   SQL Server Failover

Follow the below steps for doing the **SQL Server failover**.

1. Go to **Resource Group** -> Click on **SQL Server** resource.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a76.png)

2. Click on **Failover group** in the left side menu and click on the **failover group**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a77.png)


3. Click on **Failover** to failover group to failover.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a78.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a79.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a80.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a81.png)

4. Here you can see the secondary resource as **primary role**.    

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a82.png)

####    Re-Deploy the Region-2 ARM Temple

1.	Go to the **GitHub** and select **re-deploy.json** file from **master branch**. Copy the re-deploy.json template.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a83.png)

2.	Click on **Add** in existing Resource Group.

 ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d13-1.PNG)
    
![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d13-2.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d14.png)

4.    The **Edit template** page is displayed as shown in the following figure.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d15.png) 

5.    **Replace / paste** the template and click **Save** button.

   ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a87.png)
    
  
  ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a88.png)
    
   ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a89.png)
    
   ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a90.png)
    
   ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a91.png)

####    Verifying the Web Application 

1.	Go to **Resource Group** -> Click on **first Traffic Manager** from the below resources. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a59.PNG)

2.	Copy the **Traffic Manager URL** and open it in browser.  

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/admin92.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a93.png)

3.	Enter **Azure AD Authorized User Credentials**. 

User ID: *******@sysgain.com  

Password: ******************  

After successful validation by the **Azure AD**, based on the user role the web app will redirect you to **Admin Page** 
  
  ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/view.png)

4.	Click on **document icon** in the **shipment tab**, it will expand a section where you can upload your documents. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a94.png)

5.	Click on **Choose Files Button** which will open a window for you to select the file.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a95.png)

6.	Once the file is uploaded, you will see **File Uploaded Successfully** message as below.  

7.	The next step is to upload document information to the **Blockchain**. For this, select the Document Type from the drop-down list.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a96.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a97.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a98.png)

8.	Click on **Upload to Blockchain** button which will upload the document information in the **Blockchain**. After successful upload, you will see a response as below.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a99.png)

9.	When you click the **View Document Button**, a section gets expanded below the ribbon where you will be able to see a table which contains a list of documents against the respective shipment. The expanded section is highlighted in the below image.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a100.png)

10.	When you click on view icon button you will be able to view the document in the new tab or it will get downloaded if the file extension is other than **.pdf**

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a101.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a102.png)

11.	To check if the status of the shipment is updated or not, click on **shipment ID** of the ribbon as shown below.  

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a103.png)

12.	This will open the dashboard of that respective shipment where you can check the status value under **Shipping Details** Sections as shown below.  

13.	To check whether the record of shipment status is recorded in **Blockchain** or not, you can simply check the **Blockchain Transactions** sections under the **Shipping Details** sections where all the transaction made to the **Blockchain** are shown in chronological order.  

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a104.png)
    

14.	Click on the **transaction hash** which will show the **transaction details** in a modal as below.  

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a105.png)

15.	The **Tracker Tab** will be rendered which will show the last known location of the shipment. The view of this tab is shown above. When you click on the marker, a pop-up will be display next to the marker that will show **shipment details** and incidents.  

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a106.png)


16.	The **Status Tab** will show a list of objects along with their **Object ID, Beacon ID**, the object it is associated with, **Temperature, Humidity, Shock and Vibration Alerts, and count of incidents**.  

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a107.png)


17.	The **Devices Tab** will consist of a list of association of beacons and objects with **Gateways**. The connectivity status of the devices will also be shown in this list.  

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a108.png)

18.	The **Incidents Tab** consists of a list of all the alerts that has occurred over the course of monitoring the shipment. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a109.png)

19.	This tab shows all the alerts that are stored in **Blockchain**. All the information regarding the alert will be shown in this tab along with **Alert Starting Time and Alert Ending Time**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a110.png)

20.	Here you can see the whatever you added Beacons and Sensor data. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a111.png)

21.	Here you check the Device twin connected or not. 

**NOTE**:  If the data is not coming to web app you can verify the following components to troubleshoot the issue. 

22.	Go to **Resource Group** -> Click on **IoT hub**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a62.PNG)

23.	Click on **IoT devices** in the left side menu.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a113.png)

24.	Click on **Device ID**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a114.png)

25.	Click on **Device twin**, here you can see the Status of the device.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a115.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a116.png)

26.	And check the **Message count** is increasing or not.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a117.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a118.png)

27.	Go back to the **Resource Group** -> Click on **Cosmos DB**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a119.png)


28.	Click on **Data Explorer** in the left side menu.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a120.png)

29.	Here you can check the latest transaction message/document.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a121.png)

30.	Go to **Resource Group** -> Click on **Stream analytic**

   ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a56.PNG)

31.	Here you can see the increasing **Input Events and Output Events**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a123.png)
    
    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a124.png)


32.	Go back to **Resource Group** -> Click on **SQL database**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a125.png)

33.	Click on **Query editor** in the left side menu.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a126.png)

34.	Enter the following credentials to open the **SQL database**.

**Credentials**:

Login: sqluser

Password: Password@1234

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a127.png)

35.	Here you can see the latest stored record.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a128.png)

####    Premium Solution Type

#####   Accessing the web application

1.	Go to **Resource Group** -> Click on **Traffic Manager** from the below resources

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a59.PNG)

2.	Copy the **DNS name** and open it in browser. 

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a130.png)

3.	Now you can see the landing page of **Web Application**.

    ![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/a131.png)

After opening the web application, you can verify the application flow(use case) like Device Onboarding, Shipment Creation, Reports

#####   Premium Solution Application HA

To perform HA when the **primary region fails**, we need to use **secondary region** (DR) components from the **same resource group** where all DR components were deployed as part of the **Premium solution** as discussed in **Exercise 4, Task 3, Application HA**.

#####   Performing DR Strategies 

Perform the IoT Hub, Cosmos DB, Azure SQL DB and Stream Analytics failovers as discussed in section **Exercise 4, Task 4** and Verify the application flow as discussed in  **Verifying the Web Application under Task 4**
