<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDP, DNS, DHCP, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 22.04

<h2>High-Level Steps</h2>

- Create a resource group
- Create a Windows 10 virtual machine
- Create a Linux (Ubuntu) virtual machine
- Make sure both virtual machines are in the same virtual network and subnet
- Connect to Windows 10 virtual machine
- Install and open Wireshark on Windows 10 virtual machine
- Observe network traffic

<h2>Actions and Observations</h2>
Create a resource group

- In Azure, browse to "Resource Groups"
- Click "Create" and fill out necessary fields
- Review and create your resource group


<p>
  
![image](https://github.com/user-attachments/assets/0a217964-ccc9-4cf6-bdeb-216f808d4bdd)

</p>
<p>


</p>
<br />

Create a Windows 10 Virtual Machine
- In Azure, browse to "Virtual Machines"
- Click "Create" then select "Azure Virtual Machine"
- Under "Resource group", select the resource group you just created
- Under "Image", select the Windows 10 Pro option
- Review and create your virtual machine

<p>
  
![image](https://github.com/user-attachments/assets/62033d65-bdef-4899-b46a-ecab64cd8709)

</p>
<p>

Create a Linux(Ubunutu) Virtual Machine
- In Azure, browse to "Virtual Machines"
- Click "Create" then select "Azure Virtual Machine"
- In "Resource group", select the same resource group you had just created
- In "Image", select the Ubuntu Server 22.04 LTS 
- In "Authenication type", fill out your selected username and password
- Scroll to the "Networking" tab, and under "Virtual network", select the virtual network you created when creating the Windows 10 VM
- Review and create your virtual machine



<p>
  
![image](https://github.com/user-attachments/assets/20263cc4-fbb9-4158-9af4-5cecf414dda3)

</p>
<p>
  
Make sure both virtual machines are in the same virtual network/subnet
- In Azure, navigate to "Virtual Machines"
- Click on your Windows virtual machine and check the name of the "Virtual network/subnet"
- Click on your Linux virtual machine and make sure the "Virtual network/subnet" is the same as in your Window virtual machine (Ex: windows-vm-vnet)

</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/18c9fc89-5b29-4b5b-9b92-34deeb4d15e4)

</p>
<p>

Connect to Windows 10 Virtual Machine
- Open up Remote Desktop to connect to the Windows 10 VM,
- To find the the public IP Address of the Windows 10 VM, go to Azure, scroll to your Windows VM and look for its "Public IP Address"
- Copy the public IP address and paste it into the "Computer" field in your Remote Desktop App and connect

</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/e7e90063-37bd-4336-bc7b-4f5d26d2ebe0)

</p>
<p>

Install Wireshark inside the Windows 10 VM
- In your Windows 10 VM, open up the browser, and download and install Wireshark and open it


Observe the network traffic
- Open PowerShell so we can observe the network traffic
- In Wireshark, start packet capture by clicking the blue fin at the top left

<p>
  
![image](https://github.com/user-attachments/assets/563ebd10-5c67-4915-baa6-de1cdd8819d0)

</p>
<p>

</p>
<br />

Lets observe ICMP traffic
- In Wireshark, type "ICMP" in the search bar and press Enter to add a filter that will only display ICMP traffic
- In Azure, retrieve the private IP address for the Linux(Ubuntu) virtual machine 
- After acquring the private IP address, we are going to attempt to ping from within the Windows 10 VM
- In PowerShell type "ping" followed by the Linux private IP address Ex: "ping 10.0.0.5"
- Observe ping requests and replies in Wireshark

<p>
  
![image](https://github.com/user-attachments/assets/687588c5-0205-4dc4-b09e-2e7979292643)

</p>
<p>

</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/c25301bc-8178-4d66-94e6-f679119f8d55)

</p>
<p>

</p>
<br />



Ping a public website in PowerShell and observe the traffic Ex: "ping www.google.com"

<p>
  
![image](https://github.com/user-attachments/assets/5dce1e5e-4a47-4c45-8c2c-04cafc769867)

</p>
<p>

</p>
<br />

Start a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM, type "-t" at the end of the ping Ex: "ping 10.0.0.5 -t" and observe the traffic

<p>
  
![image](https://github.com/user-attachments/assets/a914de4c-7123-4bac-822e-bfdd807142e7)

</p>
<p>

</p>
<br />

Open the Network Security Group(NSG) that your Linux(Ubuntu) VM is using within Azure and disable incoming ICMP traffic by creating a port rule that blocks ICMP traffic

<p>
  
![image](https://github.com/user-attachments/assets/1d4c6274-1d32-48f4-a527-71336de16463)

![image](https://github.com/user-attachments/assets/59587692-2ac2-4d2b-b479-98c7c3259ccf)

</p>
<p>

</p>
<br />

Unblock the ICMP traffic for the Network Security Group in your Ubuntu VM and back in the Windows 10 VM, watch the ICMP traffic in WireShark and the command line ping activity it should start working again. Finally, stop the ping activity

<p>
  
![image](https://github.com/user-attachments/assets/31281179-9fc6-4dd4-9381-4ebef57806e0)

</p>
<p>

</p>
<br />



<p>
  

</p>
<p>

</p>
<br />


Time to observe SSH traffic

- Inside Wireshark, type in "SSH" in the search bar and press enter to apply a filter that will only show SSH traffic
- "SSH into" your Linux(Ubuntu) VM through its private IP address by typing "ssh (username)@(private IP address)" in PowerShell Ex: "ssh labuser@10.0.0.5")
- In PowerShell, type the commands (hostname, id, etc) into the Linux(ubuntu) SSH connection and observe traffic


- Exit the SSH connection by typing exit and pressing return

<p>
  
![image](https://github.com/user-attachments/assets/4b595f46-190c-4993-b605-632a1891f09f)

</p>
<p>

</p>
<br />

Observe DHCP Traffic
- In Wireshark, filter for DHCP traffic only. In your Windows 10 VM, try to give your VM a new IP address from the command line (ipconfig /renew)
- Observe the DHCP traffic appearing in WireShark

<p>
  
![image](https://github.com/user-attachments/assets/47f8014a-1b0c-428f-864e-0f32366d28c8)

</p>
<p>

</p>
<br />

Observe DNS traffic
- In Wireshark, filter for DNS traffic only
- In your Windows 10 VM in the command line, use nslookup to see what google.com and disney.com’s IP addresses are and observe the DNS traffic being shown in WireShark

<p>
  
![image](https://github.com/user-attachments/assets/3680cc10-7f08-4634-ad75-b3cd83984d61)

</p>
<p>

</p>
<br />


Observe the RDP traffic

- In Wireshark, filter for RDP traffic only using "tcp.port==3389" and observe the traffic
- Observe that traffic is non-stop because the RDP protocol is constantly showing a live stream from one computer to another, so traffic is always being sent

<p>
  
![image](https://github.com/user-attachments/assets/16b053b4-5f95-4dea-ac76-5bc9592daef1)

</p>
<p>

</p>
<br />  





Congratulatons on completing the assignment!!! Hopefully this helps you understand network performance, troubleshoot connectivity issues, and enhance security by enforcing strict traffic filtering rules.
<p>
  


</p>
<p>

</p>
<br />
