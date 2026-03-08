<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Remote Desktop
- Microsoft Azure (Virtual Machines/Compute)
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (22H2)
- Ubuntu Server 22.04

<h2>High-Level Steps</h2>

- How to use Remote Desktop
- Create Resource Group
- Create Windows 10 Virtual Machine (VM)
- Create Linux Virtual Machine (VM)
- Download Wireshark
- Observe ICMP Traffic
- Configure Firewall (Network Security Group)

<h2>Actions and Observations</h2>

<p>
<img width="1094" height="701" alt="Screenshot 2026-03-07 172833" src="https://github.com/user-attachments/assets/61e055ad-a361-42e0-a8cc-d426a3fc5ac1" />
</p>
<p>
To connect to another computer or virtual machine using Remote Desktop, first make sure the remote computer has Remote Desktop enabled and that you have permission to access it. On your computer, open the Start menu, search for Remote Desktop Connection, and open the application. In the Computer field, type the IP address of the remote computer you want to connect to. Click Connect, and when prompted, enter the username and password for the account that has access to that computer. After you enter the credentials, click OK, and the Remote Desktop session will open, allowing you to control the remote computer as if you were sitting in front of it.
</p>
<br />

<p>
<img width="1092" height="702" alt="Screenshot 2026-03-06 174808" src="https://github.com/user-attachments/assets/1ef8c087-86cd-4799-8ca3-6e6054a42f7a" />
</p>
<p>
To create a Resource Group in Microsoft Azure, first sign in to the Azure Portal. In the search bar at the top of the portal, type Resource groups and select it from the results. On the Resource Groups page, click Create, next select the subscription you want to use, then enter any Resource group name you choose (example, RG-Network-Activities). Choose a Region, which determines where the group’s metadata will be stored. After entering the required information, click Review + Create, then click Create again. Once the deployment finishes, the new resource group will appear in your Azure portal and can be used to organize and manage related resources such as virtual machines, storage accounts, and networks.
</p>
<br />

<p>
<img width="1089" height="704" alt="Screenshot 2026-03-07 130430" src="https://github.com/user-attachments/assets/35988661-19b8-4884-b06a-b837ffdfce77" />
</p>
<p>
To create a Windows 10 virtual machine (VM) in Microsoft Azure, first sign in to the Azure Portal. In the search bar at the top, type Virtual Machines and select it from the results. On the Virtual Machines page, click Create, then choose Azure virtual machine. On the Basics tab, select your subscription, choose or create a resource group (example RG-Network-Activities), and enter a virtual machine name of your choice (example windows-vm). Next, select the region where the VM will be hosted and choose an Image (for example, Windows 10). Select a VM Size based on the CPU and memory you want (example Standard_D2s_v3 - 2 vcpus, 8 GiB memory). Under the Administrator account, create a username and password to sign in to the VM. Make sure Remote Desktop (RDP) is allowed so you can access the machine later. Near the bottom of the page, select Licensing by placing a check. On the Networking tab, to rename the Virtual network, click Create new, then enter a name of your choice (example Lab2-Vnet). When ready to deploy the VM, click Review + Create, then click Create. Azure will deploy the virtual machine, and once the process is complete, you can connect to it using Remote Desktop from the VM’s public IP address.
</p>
<br />

<p>
<img width="1093" height="704" alt="Screenshot 2026-03-07 123937" src="https://github.com/user-attachments/assets/d8eb0521-d4ec-46d2-aa84-b044ca706a54" />
</p>
<p>
To create a Linux virtual machine (VM) in Microsoft Azure, first sign in to the Azure Portal. In the search bar at the top, type Virtual Machines and select it from the results. On the Virtual Machines page, click Create, then choose Azure virtual machine. On the Basics tab, select your subscription, choose or create a resource group (example RG-Network-Activities), and enter a virtual machine name of your choice (example linux-vm). Next, select the region where the VM will be hosted, and if you want this Linux VM to share a virtual network, make sure this region matches with other VMs you have deployed. Next, choose an Image (for example, Ubuntu Server 22.04). Select a VM Size based on the CPU and memory you want (example Standard_D2s_v3 - 2 vcpus, 8 GiB memory). Under the Administrator account, for Authentication type select Password, then create a username and password to sign in to the VM. Make sure Remote Desktop (RDP) is allowed so you can access the machine later. Now, click Next until you reach the Networking tab. To rename the Virtual network, click Create new, then enter a name of your choice, or if you want to use the same virtual network, enter the same name here (example: Lab2-Vnet). When ready to deploy the VM, click Review + Create, then click Create. Azure will deploy the virtual machine, and once the process is complete, you can connect to it using Remote Desktop from the VM’s public IP address.
</p>
<br />

<p>
<img width="494" height="382" alt="Screenshot 2026-03-07 174215" src="https://github.com/user-attachments/assets/e57f596b-fe5b-47e0-acd2-e66624ece470" />
</p>
<p>
To download the Windows x64 installer for Wireshark, open a web browser and go to the official Wireshark website at "https://www.wireshark.org". On the homepage, click the Download button. Under the Windows section, look for the option labeled Windows x64 Installer (this is the 64-bit version for most modern Windows computers). Click the link, and the installer file will begin downloading. Once the download is complete, you can open the file from your browser’s download bar or your Downloads folder to begin the installation process. To install Wireshark, simply click Next through each setup window, then click Install when prompted, without changing or selecting any additional options.
</p>
<br />

<p>
<img width="959" height="520" alt="Screenshot 2026-03-07 181321" src="https://github.com/user-attachments/assets/64265ebe-c328-4ba3-9b71-e926971839a1" />
</p>
<p>
To observe ICMP ping traffic between two virtual machines using Wireshark, first open Wireshark on the VM where you want to capture the network traffic (for example, a Windows VM). In the Capture section, click Ethernet once to select the active network adapter. Next, click the shark fin icon under the File menu to begin capturing packets. Once packet capture starts, go to the Apply a display filter field at the top and type icmp, then press Enter to display only ICMP traffic.

Next, open PowerShell by using the Search option in the Start menu on the Windows VM. In PowerShell, type the command ping followed by the private IP address of the second VM (for example, a Linux VM), such as ping 10.0.0.5. The ping results will appear in PowerShell, showing the number of packets sent and received. If the Packets Sent and Packets Received numbers match, the ping was successful. At the same time, Wireshark will display the ICMP Echo Request and Echo Reply packets generated by the ping.
</p>
<br />

<p>
<img width="1247" height="672" alt="Screenshot 2026-03-07 185333" src="https://github.com/user-attachments/assets/8f50eec2-8aa8-4f59-b964-b4ce47115666" />
</p>
<p>
To configure the firewall using a Network Security Group (NSG) in Azure, first open the virtual machine you want to configure (for example, linux-vm) in the Azure portal. Select Networking, then click Network settings. Under the Network security group section, click the name of the NSG attached to the VM. Once the NSG page opens, go to Settings, select Inbound security rules, and click Add to create a new rule.

In the new rule settings, leave Source set to Any and Destination set to Any. For Destination port ranges, enter an asterisk (*), which represents any port. Under Protocol, select ICMPv4, and under Action, choose Deny so that ICMP ping requests will be blocked. Next, set the Priority to 290 so the rule takes precedence over lower-priority rules. After entering these settings, click Add to create the rule. Once the rule is applied, try sending another ICMP ping from the primary VM (example Windows VM). The ping request should now fail with "Request timed out", indicating that the firewall rule is successfully blocking the traffic.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

