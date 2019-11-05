# Post-Deployment Steps for Cold Chain Solution

## Table of Contents

[Overview](#Overview)

[Pre-Requisites](#Pre-requisites)

[Exercise 1: Deploy smart contract and getting the Contract Address](#exercise-1-deploy-smart-contract-and-getting-the-contract-address)

## Overview

Secure Cold Chain solution for Pharma addresses the challenges and concerns of the pharmaceutical companies, by providing near real-time tracking of the temperature sensitive consignments in a transparent and immutable manner throughout the supply chain, by combining IoT and Blockchain. The solution provides actionable insights for all the stakeholders through real time data capture, comprehensive analytics and immutable access with increased granularity (product, box, carton, or pallet level), thus helping in achieving business transformation and reaping the associated benefits.

### Scenario and Objectives

You were asked to deploy the smart contract in the Quorum blockchain and get the contract address.

After completing this lab, you will be able to:

*	Understand the steps to deply a smart contract

*	How to create NAT rules

*  Understand the fucntion of Load Balancer


## Pre-Requisites

* Azure Portal access with Owner permission.
* Familiar with Quorum Blockchain services.

**Note:** You should have access to Azure portal with Owner permission to complete this Training Lab

## Exercise 1: Deploy smart contract and getting the Contract Address

**Scenario**

This exercise explains how to deploy Deploy smart contract and getting the contract Address.

The main tasks for this exercise are as follows:
 
1.	Associating NAT rule of port 8545 to the BM0 Machine

2.	Deploying smart contract and getting the Contract Address


### Task 1: Associating NAT rule of port 8545 to the BM0 Machine

1. Click on **Load Balancer** resource and click on **Inbound NAT rules** in left side.

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de10.PNG)

2. Click on **NatBM0_RPC_Port** rules

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de11.PNG)

3. Click on Dropdown **Target virtual machine** to **BMO** and **Network IP configuration** to **BM0** and click **Save**

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de12.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de13.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de14.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/de15.PNG)

### Task 1: Deploy smart contract and getting the Contract Address

1.Go back to the **Load Balancer** and copy IP Address and port: **3000** paste it in to the putty.

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

#### Running Blockchain servic in TMT-VM

After the contract deployment you have to perform the following steps to run the block chain cron job service in tmt-vm.

For that you have to provide the following values from the output section of the ARM and provide it to the following script url.

Refer output section from the ARM deployment for the Blockchain IP or FQDN.

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

    **wget <https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/scripts/blockchain-service.sh>**
    
    **cat blockchain-service.sh | tr -d '\r' > blockchain-service.sh1 | mv blockchain-service.sh1 blockchain-service.sh**
    
    **sudo chmod 777 blockchain-service.sh**
    
    ./blockchain-service.sh &lt;Blockchain IP&gt; &lt;Password&gt; &lt;contractAddress&gt; &lt;Gas Limit&gt;

**Ex**: ./blockchain-service.sh "52.175.243.187" "Password@1234" "0xd761de896114f745e5ef789532523ff9ab3cf553" "4000000"

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d60-7.PNG)

![alt text](https://raw.githubusercontent.com/SecureColdChain/Wipro-Ltd-ColdChain/master/Documentation/images/d60-8.PNG)
