<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Create a resource group
- Create a Windows 10 virtual machine
- Create a Linux(Ubuntu) virtual machine
- Make sure both virtual machines are in the same virtual network/subnet
- Connect to Windows 10 virtual machine
- Install and open Wireshark on Windows 10 virtual machine
- Observe network traffic
- Clean up Azure environment

<h2>Actions and Observations</h2>
Create a resource group

- In Azure, navigate to "Resource Groups"
- Click "Create" and fill out necessary fields
- Review + create your resource group


<p>
  
![image](https://github.com/user-attachments/assets/0a217964-ccc9-4cf6-bdeb-216f808d4bdd)

</p>
<p>


</p>
<br />

Create a Windows 10 Virtual Machine
- In Azure, navigate to "Virtual Machines"
- Click "Create" then select "Azure Virtual Machine"
- Under "Resource group", select the resource group you just created
- Under "Image", select the Windows 10 Pro option
- Review + create your virtual machine

<p>
  
![image](https://github.com/user-attachments/assets/62033d65-bdef-4899-b46a-ecab64cd8709)

</p>
<p>

Create a Linux(Ubunutu) Virtual Machine
- In Azure, navigate to "Virtual Machines"
- Click "Create" then select "Azure Virtual Machine"
- Just like in the previous step, under "Resource group", select the same resource group you had just created
- Under "Image", select the Ubuntu Server 22.04 LTS 
- Under "Authenication type", select "password" and fill out your chosen username and password
- Navigate to the "Networking" tab, and under "Virtual network", select the virtual network you created when creating the Windows 10 virtual machine
- Review + create your virtual machine



<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
  
Make sure both virtual machines are in the same virtual network/subnet
- In Azure, navigate to "Virtual Machines"
- Click on your Windows virtual machine and check the name of the "Virtual network/subnet"
- Click on your Linux virtual machine and make sure the "Virtual network/subnet" is the same as in your Window virtual machine

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

Connect to Windows 10 Virtual Machine
- Open up Remote Desktop to connect to the Windows 10 virtual machine,
- We need to find the Public IP Address to fill in the "Computer" field of Remote Desktop
- To retrieve the public IP Address of the Windows 10 virtual machine, go to Azure, navigate to your Windows virtual machine and look for its "Public IP Address"
- Copy the public IP address and paste it into the "Computer" field in your Remote Desktop Application and connect

</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

Install wireshark inside the Windows 10 VM
- IN your Windows 10 virtual machine, open up Microsoft Edge, and download and install Wireshark
- Open Wireshark

Observe the network traffic
- Open Microsoft Windows PowerShell as we prepare to observe network traffic
- In Wireshark, start packet capture by clicking the blue fin icon at the top left(under the "File" button)

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

ICMP Traffic
- In Wireshark, type in "ICMP" in the search bar and hit Enter to apply a filter that will only display ICMP traffic
- In Azure, retrieve the private IP address for the Linux(Ubuntu) virtual machine you created the same way you retrieved the Windows 10 public IP address
- After retrieving the private IP address, we are going to attempt to ping from within the Windows 10 virtual machine
- Within PowerShell type "ping" followed by the Linux private IP address (example. "ping 10.0.0.5")
- Observe ping requests and replies within Wireshark

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

Attempt to ping a public website within PowerShell and observe traffic (example. "ping www.google.com")

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM, type "-t" at the end of the ping (example. "ping 10.0.0.5 -t") and observe traffic

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

Open the Network Security Group(NSG) your Linux(Ubuntu) virtual machine is using within Azure and disable incoming ICMP traffic by creating a port rule that denies ICMP traffic

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic, while back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity:

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />


<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

Re-enable ICMP traffic for the Network Security Group in your Ubuntu VM and back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line ping activity (should start working again).Finally, stop the ping activity:

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />


Time to observe SSH traffic

- In Wireshark, filter for SSH traffic only and from your Windows 10 VM, “SSH into” your Ubuntu virtual machine (via its private IP address). Type commands (ls, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark.

- Exit the SSH connection by typing ‘exit’ and pressing [return]

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

Observe DHCP Traffic
- In Wireshark, filter for DHCP traffic only. From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
- Observe the DHCP traffic appearing in WireShark

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

Observe DNS traffic
- In Wireshark, filter for DNS traffic only
- In your Windows 10 VM inside the command line, use nslookup to see what google.com and disney.com’s IP addresses are and observe the DNS traffic being shown in WireShark

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />


Observe the RDP traffic

- In Wireshark, filter for RDP traffic only using "tcp.port==3389".
- Observe traffic
- Notice that traffic is non-stop because the RDP protocol is constantly showing a live stream from one computer to another, so traffic is always being transmitted

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />  




Clean up you Azure Enviroment 

- Close your Remote Desktop connection, delete the Resource Group(s) created at the beginning of this tutorial, and verify Resource Group deletion. 

