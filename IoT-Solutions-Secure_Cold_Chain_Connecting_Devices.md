# IoT-Solutions-Secure Cold Chain:Connecting Devices to the Solution

## Table of Contents

[Overview](#Overview)

[Pre-Requisites](#Pre-requisites)

[Exercise 1: TMT250 Device Configuration](#exercise-1-tmt250-device-configuration)

[Exercise 2: Connecting Rigado Cascade500 IoT Gateway](#exercise-2-connecting-rigado-cascade500-iot-gateway)

[Exercise 3: Connecting Beacons](#exercise-3-connecting-beacons)
 
## Overview

Secure Cold Chain solution for Pharma addresses the challenges and concerns of the pharmaceutical companies, by providing near real-time tracking of the temperature sensitive consignments in a transparent and immutable manner throughout the supply chain, by combining IoT and Blockchain. The solution provides actionable insights for all the stakeholders through real time data capture, comprehensive analytics and immutable access with increased granularity (product, box, carton, or pallet level), thus helping in achieving business transformation and reaping the associated benefits.

### Scenario and Objectives

You were asked to configure the different devices used in this solutions.

After completing this lab, you will be able to:

* understand how to configure TMT-250 Device for GPS tracking

* understand how to connect Rigado Cascade-500 IoT Gateway to the cloud

*  understand how to coonect Beacons to send the telemetry data


## Pre-Requisites

* Azure Portal access with Owner permission.
    
* You need to have the following devices :
     1. Raspberry Pi3
     2. Teltonika TMT -250
     3. Rigado Cascade-500 IoT Gateway
     4. Beacons
* You need to complete the following lab before attempting this lab 
  
  IoT-Solutions-Secure Cold Chain: Build the Web App code

* Familiar with Azure IoT services and Device configurations. 

**Note:** You should have access to Azure portal with Owner permission to complete this Training Lab

## Exercise 1: TMT250 Device Configuration

**Scenario**

This exercise explains about how to configure TMT-250 for GPS tracking.

The main task for this exercise is:

1.	 TMT250 Device Configuration

### Task 1:  TMT250 Device Configuration

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

## Exercise 2: Connecting Rigado Cascade-500 IoT Gateway

**Scenario**

This exercise explains about how to connect Rigado Cascade-500 IoT Gateway to the solution.

The main tasks for this exercise is:

1. Connecting Rigado Cascade-500 IoT Gateway

### Task 1:  Connecting Rigado Cascade-500 IoT Gateway

1.	Connect **LAN cable** to the **Rigado** and switch on it.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d94.png)

## Exercise 3: Connecting Beacons

**Scenario**

This exercise explains about how to connect Beacons to the solution.

The main tasks for this exercise is:

1. Connecting Beacons

### Task 1:  Connecting Beacons

1.  Switch on the **Beacons (Sensor)** and keep it within the range of **Rigado.**

    Note: If Beacon will show **Red light,** it is in **ON** state otherwise **OFF** state

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d95.png)

Press **ON** the **beacon 3 times,** at that time if it shows **Red light,** it is in **ON** state otherwise it shows **Green light,** it is in **OFF** state.
