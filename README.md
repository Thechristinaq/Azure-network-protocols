<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols 
- Wireshark (Protocol Analyzer)
- Powershelll (Command Line Interface)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Create Two Virtual Machines in Azure
- Step 2: Remote Desktop into VMs
- Step 3: Install and Run Wireshark
- Step 4: Test Connectivity Between VMs
- Step 5: Alter Network Security Group Settings
- Step 6: SSH into VM
- Step 7: Observe DHCP Traffic 

<h2>Actions and Observations</h2>

Step 1: Create Two Virtual Machines in Azure
<br> - In the Microsoft Azure Portal, search "Resource groups" in the search bar and create a Resource group
<br> - Search "Virtual Machines" in the search bar and create two Virtual Machines with the following OS, Windows 10 22H2 OS for VM1, and Ubuntu 20.04 OS for VM2
<br> - Make sure when you are creating these two VMs that they are in the same Resource Group
<br> - When setting up your VMs, remember the username and password that you use, you will need this information to connect remotely into the VMs

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/a9a3ba98-8a3d-4525-9b96-912afdeafe8c)

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/63b12174-d9be-4d5f-9c30-d93d384a8961)

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/b744a959-c8d1-4c9f-a03f-2d92394612e4)


Step 2: Remote Desktop into VMs
<br> - After you have created your two Virtual Machines, you will use the Remote Desktop Connection application to connect into VM1
<br> - You can find this in the start menu search bar by typing "Remote Desktop Connection" 
<br> - You will need the Public IP address of VM1 and the username and password you created to access VM1

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/a0b1267b-b229-4bff-ab21-954ffabed1ce)

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/f87a70ba-a0b7-4086-b336-2f8252bd02b9)

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/f6c00f6d-4cb7-49fd-99e0-a9adf00ccb3c)


Step 3: Install and Run Wireshark
<br> - Once inside VM1, google Wireshark and download the application (Windows Installer 64 bit) from the official site
<br> - Once downloaded, open Wireshark and double click Ethernet 2 
<br> - Filter out the network traffic by typing "icmp" in the display filter bar 

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/dbd0e6e3-fa52-4094-aacb-eb8a93ec7f5c)

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/c98fdcd5-0fbd-4fdc-aac4-58124743ade7)

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/5dc60bed-bde5-4c66-afac-bd9b0d4e9ccd)


Step 4: Test Connectivity Between VMs
<br> - In VM1, Search Powershell in the start menu search bar and open it 
<br> - In the Azure portal, go to VM2 and copy the private IP address 
<br> - In VM1 within Powershell, type "ping -t" with VM2's private IP address to start a perpetual ping 
<br> - Wireshark will now show the two VMs pinging back and forth showing the data being communicated between both the VMs 

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/719ac2de-70c4-4fac-8691-fb9066abbe99)

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/efcee531-4b97-4ad6-9a95-893314d8f00f)

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/688aadc0-5653-4966-8bba-ada19dfc484d)

Step 5: Alter Network Security Group Settings
<br> - In the Azure Portal, type Network Security Group in the search bar (this is the VMs firewall)
<br> - Select VM2-NSG and click on Inbound Security Rules, add, and in the new popup window, change protocol to ICMP, and change action to deny, notice how the ping in VM1 Powershell is immediately halted due to being blcoked by VM2's firewall. 
<br> = To allow traffic again, simply follow the same steps within the Inbound Security Rule but to change action to allow, the perpetual ping will resume sucessfully as before 
<br> - Press Ctrl+C to stop ping within Powershell 


![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/5e3d51dc-173e-4ba8-ab2e-cbbcae31a5f4)

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/cc9f4ad7-1493-493a-863e-dfe5ab9d64c2)

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/02a9b8b7-1384-4571-ae35-cfd4f7b6cabd)

Step 6: SSH into VM
Step 7: Observe DHCP Traffic







