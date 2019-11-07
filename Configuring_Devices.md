# IoT-Solutions-Secure Cold Chain: Configuring Devices

## Table of Contents

[Overview](#Overview)

[Pre-Requisites](#Pre-requisites)

[Exercise 1: Building the Snap](#exercise-1-building-the-snap)

[Exercise 2: Uploading the snap to Rigado Gateway](#exercise-2-uploading-the-snap-to-rigado-gateway)

[Exercise 3: Verifying the Device Configuration](#exercise-3-verifying-the-device-configuration)

## Overview

Secure Cold Chain solution for Pharma addresses the challenges and concerns of the pharmaceutical companies, by providing near real-time tracking of the temperature sensitive consignments in a transparent and immutable manner throughout the supply chain, by combining IoT and Blockchain. The solution provides actionable insights for all the stakeholders through real time data capture, comprehensive analytics and immutable access with increased granularity (product, box, carton, or pallet level), thus helping in achieving business transformation and reaping the associated benefits.

### Scenario and Objectives

You were asked to build the snap, upload it to the Rigado Gateway and verify the device configuration.
After completing this lab, you will be able to:

*	Understand how to build a snap in Ubuntu OS using Rasberry Pi3

*	Understand how to uoload the snap using Rigado portal

*   Understand how to verify the device configurations in Azure portal


## Pre-Requisites

* Azure Portal access with Owner permission.
    
* You need to have the following devices :
     1. Raspberry Pi3
     2. Rigado Cascade-500 IoT Gateway
     3. You need to have developer account to remotely deploy your snap using https://app.rigado.com/

* Familiar with Azure IoT services and Device configurations.

**Note:** You should have access to Azure portal with Owner permission to complete this Training Lab

## Exercise 1: Building the Snap

**Scenario**

This exercise explains about how to build the snap using snapcraft.

The main tasks for this exercise are as follows:

1. Building the Snap

### Task 1: Building the Snap

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

##### Snap Building

1.	For now, the Node.js plugin for snapcraft doesn’t support a cross-platform build. Raspberry Pi is required for building the snap. For installation of Raspberry Pi follow the steps mentioned in the link <https://docs.rigado.com/en/latest/creating-apps/prereqs.html#developer-prereqs-rpi.>

1. Once Raspberry Pi is set up, login by using the following command:

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

## Exercise 2: Uploading the snap to Rigado Gateway

**Scenario**

This exercise explains about how to upload the snap using Rigado developer portal.

The main tasks for this exercise are as follows:

1. Uploading the snap to Rigado Gateway

### Task 1: Uploading the snap to Rigado Gateway

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

## Exercise 3: Verifying the Device Configuration

**Scenario**

This exercise explains about how to verify the device configuration using Azure portal.

The main tasks for this exercise are as follows:

1. Verifying the Device Configuration

### Task 1: Verifying the Device Configuration

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
