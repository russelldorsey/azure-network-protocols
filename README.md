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

- Windows 10 (24H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- How to use Remote Desktop
- Create Resource Group
- Create Windows 10 Virtual Machine (VM)
- Step 4

<h2>Actions and Observations</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
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
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
