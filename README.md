
<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1> Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Preparing AD Infrastructure in Azure
- Deploying Active Directory
- Configuring Remote Desktop and Creating Additional Users
- Group Policy and Managing Accounts 
  
<h2>Deployment and Configuration Steps</h2>

<p>
  Preparing AD Infrastructure in Azure
 <p></p>
PASTE SCREENSHOT HERE
<p>
To begin setting up Active Directory in Azure, I first create the foundational infrastructure. I start by setting up a Resource Group to keep all related resources organized. Then, I configure a Virtual Network (VNet) and Subnet, ensuring that all machines will communicate seamlessly within the same network. With the network in place, I deploy DC-1, a Windows Server 2022 virtual machine, which will serve as the Domain Controller. I set the username to labuser and the password to Cyberlab123!. Once the VM is created, I configure its Network Interface Card (NIC) to use a static private IP address, preventing IP conflicts and ensuring consistent connectivity. For easier troubleshooting during the initial setup, I log into DC-1 and temporarily disable the Windows Firewall to allow unrestricted communication.
Next, I set up Client-1, a Windows 10 virtual machine, and attach it to the same Virtual Network as DC-1 to enable proper communication. Using the same credentials (labuser / Cyberlab123!), I log into Client-1 and manually configure its DNS settings to point to DC-1’s private IP address. This ensures that Client-1 can locate the Domain Controller once I configure Active Directory. To apply these changes, I restart Client-1 from the Azure Portal. Once the VM is back online, I test connectivity by opening Command Prompt and using the ping command to verify that Client-1 can communicate with DC-1’s private IP address. I also check the DNS configuration in PowerShell by running ipconfig /all, ensuring that the DNS server is correctly set to DC-1’s private IP.
At this point, the Active Directory infrastructure is fully prepared. These virtual machines will be used for future labs, so I do not delete them. Instead, if I am done for the day and want to save costs, I go to the Azure Portal and stop the VMs, preventing unnecessary charges while keeping the setup intact for the next session</p>
<br />

<p>
Deploying Active Directory
<br />


<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
To continue setting up Active Directory, I first ensure that DC-1 and Client-1 are powered on in the Azure Portal if they were previously stopped. I begin by logging into DC-1 and installing Active Directory Domain Services (AD DS). Once the installation is complete, I promote DC-1 as a Domain Controller and create a new forest with the domain name mydomain.com (which I remember for future use). After the system restarts, I log back into DC-1 using mydomain.com\labuser. Next, I create a Domain Admin user by opening Active Directory Users and Computers (ADUC) and setting up two Organizational Units (OUs): _EMPLOYEES for standard user accounts and _ADMINS for administrative users. I then create a new user, Jane Doe, with the username jane_admin and the password Cyberlab123!, adding her to the Domain Admins Security Group to grant administrative privileges. To apply these changes, I log out and then log back into DC-1 as mydomain.com\jane_admin, which will now serve as my primary admin account.
With Active Directory deployed, I proceed to join Client-1 to the domain mydomain.com. Since Client-1’s DNS settings are already configured to point to DC-1’s private IP address, I log into Client-1 as the local admin (labuser) and manually join it to the domain, which triggers an automatic restart. Once Client-1 reboots, I return to DC-1, open ADUC, and verify that Client-1 appears under the domain. To keep devices organized, I create a new _CLIENTS OU and move Client-1 into it. Now that Active Directory is fully operational, I ensure my domain is functioning correctly. If I am done for the day, I navigate to the Azure Portal and stop the VMs to minimize costs while keeping the setup intact for future labs.</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
