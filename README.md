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
- In the Microsoft Azure Portal, search "Resource groups" in the search bar and create a Resource group

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/582317f7-0b1f-43b1-bbe5-8711124a01fa)

- Search "Virtual Machines" in the search bar and create two Virtual Machines with the following OS, Windows 10 22H2 OS for VM1, and Ubuntu 20.04 OS for VM2
- Make sure when you are creating these two VMs that they are in the same Resource Group
- When setting up your VMs, remember the username and password that you use, you will need this information to connect remotely into the VMs

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/2aa7231a-a68c-4f00-a79a-d7c546291149)


Step 2: Remote Desktop into VMs
- After you have created your two Virtual Machines, you will use the Remote Desktop Connection application to connect into VM1
- You can find this in the start menu search bar by typing "Remote Desktop Connection" 

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/a0b1267b-b229-4bff-ab21-954ffabed1ce)

- You will need the Public IP address of VM1 and the username and password you created to access VM1

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/5e5dbb2b-b2d3-49e5-97bb-6f5271f91f91)


Step 3: Install and Run Wireshark
- Once inside VM1, google Wireshark and download the application (Windows Installer 64 bit) from the official site

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/c23f76e1-9647-4dba-82cb-7e7591d99619)

- Once downloaded, open Wireshark and double click Ethernet 2 

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/ab792b66-4687-4f43-9277-d562c0a9fdbd)

- Filter out the network traffic by typing "icmp" in the display filter bar 

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/7af0fe3a-ee9b-4c25-bbd2-28d8146fb6a4)


Step 4: Test Connectivity Between VMs
- In VM1, Search Powershell in the start menu search bar and open it 

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/719ac2de-70c4-4fac-8691-fb9066abbe99)

In the Azure portal, go to VM2 and copy the private IP address 

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/4f598ed9-a5f0-4180-a529-03692a56cca0)

- In VM1 within Powershell, type "ping -t" with VM2's private IP address to start a perpetual ping 
- Wireshark will now show the two VMs pinging back and forth showing the data being communicated between both the VMs 

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/333223a0-d17e-4d8c-af91-1f7c06a3eb0e)


Step 5: Alter Network Security Group Settings
- In the Azure Portal, type Network Security Group in the search bar (this is the VMs firewall)
- Select VM2-NSG and click on Inbound Security Rules, add, and in the new popup window, change protocol to ICMP, and change action to deny, notice how the ping in VM1 Powershell is immediately halted due to being blcoked by VM2's firewall. 

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/c790bfb6-a4fe-40d5-a7e6-1910ab15e612)

- To allow traffic again, simply follow the same steps within the Inbound Security Rule but to change action to allow, the perpetual ping will resume sucessfully as before 
- Press Ctrl+C to stop ping within Powershell
  
![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/354b88d7-c007-40fd-8fe5-2ca55f2a155f)

Step 6: SSH into VM
- In Wireshark. filter for SSH traffic only 
- SSH into VM2 from VM1 via Powershell, in Powershell type "ssh (username)@VM2 Private IP address, follow the prompts, type yes, and in the password section, the password will not show up as you type but it will still register, presss enter
- You will notice as you type into powershell, SSH traffic starts to roll in  

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/83e27d14-6973-4918-b05f-77b9fe228dad)

- You can type id and other commands into the prompt or you can exit this section by typing exit then enter
  
![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/53a1da94-8ef7-4348-b2f8-f408b1592f94)


Step 7: Observe DHCP Traffic
- In Wireshark, Filter for DHCP traffic only
- In Powershell, type "ipconfig /renew into the command line to request a new IP address for VM1 (you may lose connection to the VM, if so, you can remote desktop back into it 
- You should be able to see the newly issued IP address in Wireshark

![image](https://github.com/thechristinaq/Azure-network-protocols/assets/165831241/fe771e34-085a-4198-85ea-a7bf113f30d1)







