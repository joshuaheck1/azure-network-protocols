<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Observing Network Traffic and Network Security Group (NSG) Functions between Azure Virtual Machines</h1>
In this project, we will observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>List of Prerequisites</h2>

- [Creating Virtual Machines in the Cloud](https://github.com/joshuaheck1/VM-creation)
  
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop (Windows) / Windows App (MacOS)
- PowerShell
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Step 1: Connect to Virtual Machine using RDP
- Step 2: Install Wirshark (Protocol Analyzer)
- Step 3: Observe ICMP Traffic
- Step 4: Use NSG (Firewall) to Deny Ping
- Step 5: Observe SSH and DHCP Traffic
- Step 6: Observe DNS and RDP Traffic

<h2>Actions and Observations</h2>

<h3>Step 1: Connect to Virtual Machine using RDP</h3>
<p>
<img width="900" alt="NSG2" src="https://github.com/user-attachments/assets/4feeae8a-e85d-4f16-8367-1aca1364efa6" />
 
<img width="900" alt="NSG3" src="https://github.com/user-attachments/assets/d458c1cd-87be-49e3-b9fd-f38c9cd51466" />
 </p>
<p>
- Start by logging into your Azure account and go to the Virtual Machines section. From here, we will need to start the VMs (turn them on). As shown in Figure 1, Select both VMs by checking the box and then click the "Start" button. Azure will ask, "Do you want to start all the selected VMs?" Click "Yes". *While we are here, note the Public IP for the windows-vm. We will need this later.*
</p>

<p>
- After a couple minutes, the VMs should be up and running. Confirm this before moving on by checking the status as shown in Figure 2. You can minimize the Azure window for now. We will come back to it later. Move to your device for the next couple of steps. 
</p>
<br />

<p>
<img width="900" alt="NSG5" src="https://github.com/user-attachments/assets/6a0c5af2-d3ef-47d1-a9d6-78e57981ce22" />
</p>

<p>
- From your device, you will need to open Remote Desktop (Windows) or the Windows App (MacOS). For this walkthrough, I used the Windows App because I am running MacOS. The Windows App can be found in the App Store and only takes seconds to download. As in Figure 3, once you open the Windows App, click the "+" dropdown button at the top right of your screen. Then, select "Add PC".
</p>
<br />
<p>
<img width="400" height="500" alt="NSG6" src="https://github.com/user-attachments/assets/535c8a2c-3b8a-4c20-9aca-a1615ac5c0ad" />
 </p>
<p>
- Enter the Public IP address for the windows-vm in "PC name". Good thing we noted the Public IP from Azure earlier. 😉 If you forgot to note it, simply go back to Azure and locate the Public IP on the main Virtual Machines page. (Refer to Figure 1.) Now for the Friendly name, I used "windows-vm" to keep it simple. Also, make sure "Reconnect if the connection is dropped" is selected. Click "Add".   
</p>
<br />

<p>
<img width="750" alt="NSG7" src="https://github.com/user-attachments/assets/9a30c7fe-277d-4f94-855c-b8d62ab9d512" />

</p>

<p>
- Enter the Username and Password for the windows-vm that we created in Azure. Click "Continue".
</p>
<br />
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
