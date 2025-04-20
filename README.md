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

- Step 1: Connect to VM using RDP & Install Wireshark
- Step 2: Observe ICMP Traffic
- Step 3: Use NSG (Firewall) to Deny Ping
- Step 4: Observe SSH and DHCP Traffic
- Step 5: Observe DNS and RDP Traffic

<h2>Actions and Observations</h2>

<h3>Step 1: Connect to VM using RDP & Install Wireshark</h3>
<p>
<img width="850" alt="NSG2" src="https://github.com/user-attachments/assets/4feeae8a-e85d-4f16-8367-1aca1364efa6" />
 
<img width="850" alt="NSG3" src="https://github.com/user-attachments/assets/d458c1cd-87be-49e3-b9fd-f38c9cd51466" />
 </p>
<p>
- Start by logging into your Azure account and go to the Virtual Machines section. From here, we will need to start the VMs (turn them on). As shown in Figure 1, Select both VMs by checking the box and then click the "Start" button. Azure will ask, "Do you want to start all the selected VMs?" Click "Yes". *While we are here, note the Public IP for the windows-vm. We will need this later.*
</p>

<p>
- After a couple minutes, the VMs should be up and running. Confirm this before moving on by checking the status as shown in Figure 2. You can minimize the Azure window for now. We will come back to it later. Move to your device for the next couple of steps. 
</p>
<br />

<p>
<img width="850" alt="NSG5" src="https://github.com/user-attachments/assets/6a0c5af2-d3ef-47d1-a9d6-78e57981ce22" />
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
<img width="700" height="500" alt="NSG7" src="https://github.com/user-attachments/assets/9a30c7fe-277d-4f94-855c-b8d62ab9d512" />

</p>

<p>
- Enter the Username and Password for the windows-vm that we created in Azure. Click "Continue".
</p>
<br />

<p>
<img width="850" alt="NSG8" src="https://github.com/user-attachments/assets/fe98c9cc-4d8d-4ffb-b896-5beda395e160" />
</p>

<p>
- We are now connected to the windows-vm in Azure from our Home Lab using RDP! Now use windows-vm's browser, "Edge", and go to www.wireshark.org to dowload Wireshark to the VM. Wireshark is a network protocol analzyer that lets you see what's happening on your network at a miscroscopic level. We will use this tool to observe network traffic with various protocols.
</p>
<br />

<p>
<img width="850" alt="NSG12" src="https://github.com/user-attachments/assets/983c0656-581b-4fca-b7a0-1f62e3f5831d" />
</p>

<p>
- From Wireshark's website, select "Windows x64 Installer" to download. Then from downloads, Open file and run the Wireshark setup. Click "Next" and "Finish" a couple times to complete the setup.
</p>
<br />

<h3>Step 2: Observe ICMP Traffic</h3>
<p>
<img width="850" alt="NSG15" src="https://github.com/user-attachments/assets/4f381a6b-e609-486f-9fff-24519a352c79" />
</p>

<p>
- Once the installation is complete, open Wireshark. On the main screen, make sure "Ethernet" is highlighted and click on the shark fin in the top left of the screen to start our capture of network traffic.
</p>
<br />

<p>
<img width="850" alt="NSG16" src="https://github.com/user-attachments/assets/43fa5ef1-d616-4a74-8383-47a674ef866c" />
 
<img width="850" alt="NSG17" src="https://github.com/user-attachments/assets/abaad5d6-3ecc-4cb7-9448-2a51bac490f2" />
 </p>
<p>
  
<p>
- As shown on Figure 9, we can see all the traffic running over the network in the purple shaded area (top box). Who knew all this was happening?
</p>

<p>
- Now locate the Filter Bar at the top of the srceen, type in icmp and hit enter. Shown in figure 10. We will use the icmp filter to observe the network traffic as we ping the linux-vm we created in Azure. We need to locate the Private IP adrress of the linux-vm in order to ping it. So, back to Azure we go. Should be quick since we just minimized it earlier.
</p>
<br />

<p>
<img width="850" alt="NSG18" src="https://github.com/user-attachments/assets/44e86958-48be-4355-991a-f6051c54d1cf" />
</p>

<p>
- In Azure, select the linux-vm and click Networking. Shown in Figure 11. The Private IP is 10.0.0.5. Minimize Azure and go back to the windows-vm.
</p>
<br />

<p>
<img width="600" alt="NSG19" src="https://github.com/user-attachments/assets/783c18ab-0313-4052-a72b-81131b06651b" />
</p>

<p>
- On the windows-vm, click the Windows button at the bottom left of you screen. Search for PowerShell. Open PowerShell. We will use commands in PowerShell to ping the linux-vm from the windows-vm.
</p>
<br />

<p>
<img width="850" alt="NSG20" src="https://github.com/user-attachments/assets/1bed5ab6-c924-4c19-9698-49f9858fcce1" />

<img width="850" alt="NSG21" src="https://github.com/user-attachments/assets/ec3874c0-d5e6-4071-a367-9b7c5cfc5391" />
</p>

<p>
- Figure 13. With Wireshark and PowerShell open, enter the command ping 10.0.0.5 in PowerShell to ping the linux-vm. Since we have the icmp filter active in Wireshark, we are only seeing icmp traffic over the network. This filter allows us to see our windows-vm (10.0.0.4) send the request to the linux-vm (10.0.0.5) and the linux-vm send a reply back to the winows-vm. Wireshark and PowerShell both show that we just successfully tested the connection between the two VMs!  
</p>

<p>
- Now in PowerShell, initiate a perpetual ping to the linux-vm with the command ping 10.0.0.5 -t. This command tells the windows-vm to ping the linux-vm non-stop. See Figure 14. Look at all that traffic! 🚗🚙🚗🚙🚗🚙🚗🚙🚗🚙🚗🚙🚗🚙🚗🚙🚗🚙🚗🚙🚗🚙🚗🚙
</p>
<br />

<h3>Step 2: Use NSG (Firewall) to Deny Ping</h3>

<p>
<img width="850" alt="NSG23" src="https://github.com/user-attachments/assets/488a7f94-86ca-40f3-8c8d-630fedcb2493" />
</p>

<p>
- While the windows-vm and linux-vm have a super long conversation, we will pivot back to Azure, explore some Network Securiy Group functions, and set a new security rule for the linux-vm. In Vitural Machines, click the linux-vm, select Network settings, and then click "linux-vm-nsg" under Network security group.
</p>
<br />

<p>
<img width="850" alt="NSG25" src="https://github.com/user-attachments/assets/0d418eaa-dffa-4928-8b25-e364c7707981" />
</p>

<p>
- Next, select Inbound security rules and then click the "+Add" button to create a new rule. We are going to tell the Firewall to Deny inbound traffic to the linux-vm. That's right. Stop that ping. Change Source to "Any". Put an asterisk in both port ranges (asterisk = all). Select "ICMPv4" for the Protocol. (Fun Fact... ping uses ICMPv4) Action will be "Deny". Change Priority to "290". The 290 will make our new rule first priority. Then, click the "Add" button.
</p>
<br />

<p>
<img width="850" alt="NSG28" src="https://github.com/user-attachments/assets/4cc11709-adce-4a8e-be93-c97eb890a700" />
</p>

<p>
- Look at that! Our new Security Rule has been created and at the top of the list. Now we will go back to the windows-vm and see what happens. 👀
</p>
<br />

<p>
<img width="850" alt="NSG26" src="https://github.com/user-attachments/assets/d7498c96-ec40-4300-b392-c1741c262f6f" />
</p>

<p>
- Look at that! Our new Security Rule has been created and at the top of the list. Now we will go back to the windows-vm and see what happens. 👀
</p>
<br />











