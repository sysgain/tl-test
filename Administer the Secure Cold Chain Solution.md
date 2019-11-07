# IoT-Solutions-Secure Cold Chain: Administer the Solution

## Table of Contents

[Overview](#Overview)

[Pre-Requisites](#Pre-requisites)

[Exercise 1: Security](#exercise-1-security)

[Exercise 2: Monitoring](#exercise-2-monitoring)

## Overview

Secure Cold Chain solution for Pharma addresses the challenges and concerns of the pharmaceutical companies, by providing near real-time tracking of the temperature sensitive consignments in a transparent and immutable manner throughout the supply chain, by combining IoT and Blockchain. The solution provides actionable insights for all the stakeholders through real time data capture, comprehensive analytics and immutable access with increased granularity (product, box, carton, or pallet level), thus helping in achieving business transformation and reaping the associated benefits.

### Scenario and Objectives

You were asked to enable security and monitoring for Cold Chain solutions.

After completing this lab, you will be able to:

* Understand the in built security features in Azure

* Understand the monitoring feature in Azure

## Pre-Requisites

* Azure Portal access with Owner permission.
    
* Familiar with Azure IoT services and Device configurations.

**Note:** You should have access to Azure portal with Owner permission to complete this Training Lab

## Exercise 1: Security

**Scenario**

This exercise explains about how to enable security for various Azure components used in the solution.

The main tasks for this exercise are as follows:

1. Seccurity

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

## Exercise 2: Monitoring

**Scenario**

This exercise explains about how to enable monitoring for the Cold Chain solution
The main tasks for this exercise are as follows:

1. Monitoring

### Task 1: Monitoring

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

1.  Click on **Live Metric Stream** to view the incoming requests, outgoing requests, overall health and servers of web application and function app.

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
