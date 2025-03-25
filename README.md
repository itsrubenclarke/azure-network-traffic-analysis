<p align="center">
<img src="https://github.com/user-attachments/assets/9a472be7-ffac-4e40-b675-605ba418d0c0" height="40%" width="60%" alt="Microsoft Azure Logo"/>
</p>




<h1>Azure: Network Traffic Analysis With WireShark</h1>
<p> 
This project is the second amongst a collection focused on implementing Azure and Active Directory.
The goal is to create a basic lab that mirrors a real working network environment, providing me with hands-on learning and practical experience with Microsoft Azure, PowerShell and WireShark.
In this project, I will establish a connection between two virtual machines using Windows and Linux in Microsoft Azure's Cloud environment. 
This will allow me to perform a basic network traffic inspection using WireShark and implement some Network Security Group rules to block, re-enable and observe different traffic types.
</p>

<h2>Prerequisites</h2>

- <a href="https://github.com/itsrubenclarke/azure-vm-setup"> Azure: Creating a Virtual Machine </a>


<h2>Key Objectives</h2>
<p>
  <h3>Remote Connectivity</h3>
  
  -  Establish Remote Desktop Connection (RDP) between the Virtual Machines (VMs)
</p>

<p>
  <h3>Basic Network Analysis and Filtering</h3>
  
  -  Capture ICMP traffic between the Virtual Machines (VMs)
  -  Use Network Security Groups (NSG) in Azure to block and re-enable ICMP Traffic
</p>

<h3>Environments and Technologies Used</h3>

- Microsoft Azure (Virtual Machines, Networking)
- Windows App (Remote Desktop Protocol)
- Wireshark (Traffic Analysis)
- PowerShell (Command-line Operations)

<p>
  <h3>Operating Systems Used</h3>
  </p>



| **Operating System**        | **Role**               |
|----------------------------|------------------------|
| <img alt= "windows logo" src="https://i.imgur.com/KcrV0u6.png" width="20"> Windows (Windows 10 Pro) | Windows Virtual Machine |
| <img alt= "Ubuntu logo" src="https://github.com/user-attachments/assets/87cccf20-cfc6-4950-b1ec-b480d913e7eb" width="20"> Linux (ubuntu 22.04) | Linux Virtual Machine              |
<p></p>

<p>
<h1>Remote Desktop Connection</h1>
</p>


<h3><img alt= "RDP logo" src="https://github.com/user-attachments/assets/4aaa5d6e-ce8b-481f-a8da-57edc9a2917e" width="20"> Step 1: Establish Remote Desktop Connection</h3>

- Go to [Portal.azure.com](https://portal.azure.com)
- Search for "Virtual Machines" in the Azure search bar
- Select the "windows-vm" you created earlier and copy its Public IP address

- Launch your Remote Desktop Connection Application
    - Mac Users download <a href="https://apps.apple.com/us/app/windows-app/id1295203466?mt=12" target="_blank" rel="noopener noreferrer">Windows App</a> Formerly known as "Microsoft Remote Desktop"
    - Windows Users open and use Remote Desktop
- Select "Add PC"
- Choose "Add Credentials" from the drop-down and enter the credentials you created earlier, noting to accept the security prompt and proceed
- You can now establish a remote connection to your virtual machine, by right-clicking the newly added device
  
<img width="1156" alt="Add PC" src="https://github.com/user-attachments/assets/151f6ec9-b615-4ed0-a5d1-6223206b2808" />

<img width="1158" alt="Connect PC" src="https://github.com/user-attachments/assets/5774f3e0-c118-44fe-89b9-57fb4ed16075" />



<h1>Observe ICMP Traffic Using WireShark</h1>

<h3><u>Step 2: Download and Run WireShark</u></h3>

- Within your Windows virtual machine launch the Edge Browser
- Visit https://www.wireshark.org/download.html
- Download the Windows x64 Installer
- Launch the Wireshark installer
- Continue through the installation prompts
- Ensure to select the check box for install "Npcap" to allow Wireshark to capture live network data
- Launch the Wireshark Application once the installation is complete
- Select the Ethernet option which has began to display network activity
- Click the shark icon in the upper left corner of the application window to begin analysing the network traffic
- A new window will be displayed titled "Capturing from Ethernet" as shown below

<img width="1262" alt="Wireshark Launched" src="https://github.com/user-attachments/assets/2a2a75e5-0809-4342-87bb-bd40a9b23e19" />



<img width="1461" alt="image" src="https://github.com/user-attachments/assets/17d5f341-a276-4d0f-bb83-dc759b0d7cd7" />

<h3>Step 3: Confirm Connection Between Virtual Machines</h3></p>

- Using Wireshark filter for ICMP traffic
- Retrieve the private IP address of the Ubuntu Linux Virtual Machine (10.0.0.5)
- Attempt to ping Linux Virtual Machine from with the Windows 10 Virtual Machine
- Observe the ping requests and replies within Wireshark

<img width="1367" alt="Ping replies" src="https://github.com/user-attachments/assets/f49a0cdd-aeb3-4d6d-8aee-ca6ce53a7df6" />


<h3>Step 4: Perpetual Pings & Network Security Groups(Firewalls)</h3>

- Initial a perpetual(non-stop-ping) from your Windows Virtual Machine to your Linux Machine using the following command:
  - "ping 10.0.0.5 -t"
- In your Windows Virtual Machine observe the continiuos ping requests and replies between the machines in both PowerShell and Wireshark
- Return to [Portal.azure.com](https://portal.azure.com)
- Open the Network Security Group your Linux Virtual Machine is using and disable incoming ICMP Traffic


![NSG Ruling](https://github.com/user-attachments/assets/030d90e2-2538-4417-9b92-a97c03d3ad38)



<h3>Step 5: Adding an Inbound Security Rule</h3></p>

- Set the source as "any"
- Source port ranges as "*"
- Destination "any"
- Service "Custom"
- Destination port ranges "*"
- Protocol "ICMPv4"
- Action "Deny"
- Priority "290" to evaluate this rule first

<img width="1365" alt="Effective Firewall" src="https://github.com/user-attachments/assets/4fb5ca31-7a0b-4213-baab-385d260aec67" />


- In your Windows Virtual Machine, observe the Failing ping requests and timeout notices
- Re-enable the ICMP traffic for the Network Security Group your Virtual Machine is using and notice the replies begin to resume
- Stop the ping activities using "CTRL +C"

<h3>Step 6: Making an SSH Connection & Observing Traffic</h3></p>

- Within your Windows Virtual Machines PowerShell
- Enter the "SSH" followed by the private ip address of your Linux machine
- You'll be prompted for your password, enter the credentials you created earlier
- Once your connection is established you can trial running some commands like "whoami" in PowerShell with the SSH filter applied in Wireshark to observe the traffic

<img width="1388" alt="SSH Filter" src="https://github.com/user-attachments/assets/4ee0fdc8-930b-48d7-9ac9-adc2b807ad1a" />

<h1>Project Summary</h1></p>

🎉Congratulations! You have carried out your first network traffic analysis using WireShark!🎉

In this project we established a remote desktop connection between a Windows (Windows 10 Pro) Virtual Machine and a Linux (ubuntu 22.04) Virtual Machine together using the Remote Desktop Connection (RDP).
Upon completion of these we carried out a basic network traffic analysis using WireShark and implemented Network Security Groups (NSG) in Azure to disable, re-enable and observe different traffic types including ICMP and SSH.
