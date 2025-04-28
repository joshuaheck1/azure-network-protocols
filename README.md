<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination" width="450"/>
</p>

<h1>Observing Network Traffic and Network Security Group (NSG) Functions between Azure Virtual Machines</h1>
In this project, we will observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Prerequisite</h2>

- [Creating Virtual Machines in the Cloud](https://github.com/joshuaheck1/VM-creation)
  
<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Windows App (macOS)
- PowerShell
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- macOS Sequoia
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

<img width="850" alt="NSG27" src="https://github.com/user-attachments/assets/b4d40127-3623-4afa-aa9a-ac07e69aa270" />
</p>

<p>
- Figure 17 shows when the ping request starts to time out in PowerShell because of the new rule we created in the Network Security Group. 
- We can see in Figure 18 exactly when the rule took effect and started to deny the ping request from the windows-vm in Wireshark. It even has a timestamp!
</p>
<br />

<p>
<img width="850" alt="NSG29" src="https://github.com/user-attachments/assets/1e12ca49-9387-4d15-83c8-c758bb5f8778" />

<img width="850" alt="NSG30" src="https://github.com/user-attachments/assets/e4358c68-7c66-48cf-ade4-4a5c70f5ee92" />
</p>

<p>
- Now, we will visit Azure real quick and delete the security rule we created. Check the box next to our rule and click the trash can to the right. Click "Yes" to confirm. With the rule deleted, the ping from the windows-vm to the linux-vm should start back up. Lets run back to the windows-vm and check it out. 🏃‍♂️
</p>

<p>
- In Figure 20, we can see via Wireshark and PowerShell that the ping started back up. Wireshark is showing the request and reply. PowerShell is showing Replies from 10.0.0.5 again. Let's Go! (To stop the perpetual ping, press Ctrl + C in PoweShell)😏
</p>
<br />

<h3>Step 3: Observe SSH and DHCP Traffic</h3>
<p>
<img width="850" alt="SSH1" src="https://github.com/user-attachments/assets/6ea801a4-b06c-42cb-aa06-234f673d8584" />

<img width="850" alt="SSH3" src="https://github.com/user-attachments/assets/3f1ae60b-20b1-4408-8da3-baee50f63363" />
</p>

<p>
- Now we are going to observe some SSH Traffic. In Wireshark, type ssh into the filter bar and start a new capture. In PowerShell, we will create a secure connection to the linux-vm with the command ssh username@PrivateIP.(username and Private IP of the linux-vm) Example = ssh jheck1@10.0.0.5 and press enter. It will ask are you sure. Type yes and press enter again. Now, you will need to enter the password of the linux-vm. FYI... as you type in the password, it will remain blank. Type in the password and press enter. Refer to Figure 21.
</p>

<p>
- As you can see in Figure 22, we now have a secure and encrypted connection between the windows-vm and linux-vm. Look at those encrypted packets in Wireshark! 🔐 🚔
</p>
<br />

<p>
<img width="850" alt="SSH4" src="https://github.com/user-attachments/assets/c2ec353e-546e-4ee1-b89b-2f109f0d1d8f" />
</p>

<p>
- Now that we are done observing SSH traffic, simply type the command exit and press enter in PowerShell. "Connection to 10.0.0.5 closed" will appear. Next, we will look at some DHCP traffic. 
</p>
<br />

<p>
<img width="850" alt="DHCP1" src="https://github.com/user-attachments/assets/93a7227e-1e04-405f-b917-50a6e20c8efa" />

<img width="850" alt="DHCP2" src="https://github.com/user-attachments/assets/f29464d7-627b-4950-a884-708625174fe0" />
</p>

<p>
- Type dhcp into the filter bar of Wireshark and start a new capture. In Powershell, type the command ipconfig /renew and press enter. Well that wasn't very exciting at all was it? Not much happened.😒 Lets direct our attention to Figure 25 for a moment because Figure 24 was a snooze fest. 😴
</p>

<p>
- So, Figure 25. What is this all about? Well, we can't use the command ipconfig /release in PowerShell because we will loose our connection to the windows-vm. We came here to see some DHCP Traffic, so lets create some. Open the Notepad on the windows-vm. Type in, ipconfig /release and ipconfig /renew like you see in Figure 25. Now, save that in C:\ProgramData as dhcp.bat and click save. Now lets hop back over to PowerShell.
</p>
<br />
<p>
<img width="850" alt="DHCP3" src="https://github.com/user-attachments/assets/2f816a07-96d7-48d7-ab6f-7721220eb7e9" />

<img width="850" alt="DHCP4" src="https://github.com/user-attachments/assets/5a2880b1-eb24-4b33-a4f7-7c3eb7634b43" />
</p>

<p>
- In Powershell, we are going to change directories with the command cd c:\programdata and press enter. Now, list what files are in this directory with the command ls and press enter. Next, run our bat file, dhcp.bat, that we just created with the command .\dhcp.bat and press enter. See Figure 26.
</p>

<p>
- You will see the ipconfig /release and the windows-vm will disconnect for a second, but it will fire back up pretty quick once the windows-vm renews the IP. Now take a look at Wireshark and PowerShell in Figure 27. We can see the actual proccess in action! DHCP traffic as promised.🤯 Big shout out to Josh Madakor for this little trick. 🫡
</p>
<br />

<h3>Step 5: Observe DNS and RDP Traffic</h3>
<p>
<img width="850" alt="DNS1" src="https://github.com/user-attachments/assets/0ad0edf0-a43d-46e9-b477-b33e00639b76" />

<img width="850" alt="DNS2" src="https://github.com/user-attachments/assets/5aa050be-bde6-4f25-852c-1df42b6894bd" />
</p>

<p>
- Time for some DNS traffic. In the Wireshark filter bar, type in dns and start a new capture. Over in PowerShell, type in the command nslookup disney.com and press enter. PowerShell shows us the an IP for Disney. Lets copy that IP, take it the browser, and see what we get when we run a search. See Figure 28. 
</p>

<p>
- What is this? 🤨 Even Wreck-it-Ralph looks confused. We can see that the IP, 130.211.198.204, is clearly related to Disney somehow. Notice the Disney logo by the IP address? Here are a couple things to consider. 1) We probably are not authorized to see what this IP really is. 2) DNS protocol translates human-readable domain names into machine-readable IP addresses. Very few websites can be accessed by typing the IP address directly into the address bar of a browser. Still, pretty cool stuff. 
</p>
<br />

<p>
<img width="850" alt="RDP1" src="https://github.com/user-attachments/assets/7a4c3d8b-2ce0-441c-89ce-e45520c51cad" />

<img width="850" alt="RDP2" src="https://github.com/user-attachments/assets/e2370e30-1b5e-492b-bbf1-cb2b80173138" />
</p>

<p>
- Last but certainly not least. Lets look at some RDP traffic and switch it up a bit. Filter the traffic by the Port RDP uses. In the filter bar, type tcp.port == 3389 and start a new capture. Notice all the packets just zooming through? We saw this same thing at the beginning of this project. We have been running a virtual machine using RDP (Remote Desktop Protocol) this entire time! There is traffic constantly flowing over the network while we are connected to the windows-vm. Also, you can filter in Wireshark with rdp in the filter bar. See figure 31. 
</p>

<h2>Summary</h2>

<p>
This concludes our project. We sucessfully connected to our windows-vm using RDP and observed a ton of network traffic with various protocols using Wireshark and PowerShell. I highly recommed hitting the YouTube and checking out more about both. The more tools you are familiar with, the better. Hey, we even dipped our pinky toe into the vast ocean of Cybersecurity by creating a new security rule to deny inbound traffic. Maybe that was a stretch, but still fun stuff.</p> 
<p>Hopefully, you learned something that you didn't know before and possibily had a little fun at the same time. I know Wreck-it-Ralph did. Don't forget to Stop (turn off) the VMs in Azure. As always, Thank You for your time and viewing this Project. We'll see you on the next one!😎      
</p>
<br />






