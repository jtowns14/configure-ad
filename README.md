<p align="center">
<img src="https://i.imgur.com/w7amRI0.png" height="40%" width="60%"/>
</p>

<h1>Configuring On-premises Active Directory within Azure VMs</h1>In this project, I configured on-premises Active Directory and created user accounts with PowerShell within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Steps</h2>

- Create 2 virtual machines, one with Windows 10 (Client VM) and the other with Windows Server 2022 (DC/Domain Controller VM)
-	Set the DC’s NIC private IP address from Dynamic to Static
-	Connect to both VMs using Remote Desktop
-	Initiate a perpetual ping from the Client to the DC; if there is no reply, enable Core Networking Diagnostics in the DC’s firewall
-	Install Active Directory Domain Services on the DC and promote it to a domain controller
-	Create an admin account and Organizational Units (OU) in Active Directory Users and Computers (ADUC), then log back in using the admin account
-	Set the Client’s DNS settings to the DC’s Private IP address, then join the Client to the DC
-	Enable Remote Desktop for domain users to access the Client
-	Create user accounts using a PowerShell script (run PowerShell ISE as administrator)
-	Connect to the Client with Remote Desktop using one of the newly created user accounts


<h2>Synopsis</h2>

<p>
<img src="https://i.imgur.com/ti0b95l.png" height="70%" width="70%"/>
</p>
<p>
On Azure, I set up two virtual machines: one with Windows Server 2022 (designated as the Domain Controller) and the other with Windows 10 (acting as the Client). To ensure consistent DNS referencing, I changed the DC's IP setting from dynamic to static. After this, I checked their network alignment using Azure's Network Watcher, making sure they resided on the same network and subnet.
</p>
<br />

![image](https://github.com/jtowns14/configure-ad/assets/139197948/77736aee-f097-47e4-add7-e266b361896e)


<p>

</p>

![image](https://github.com/jtowns14/configure-ad/assets/139197948/b6ca6290-51e5-4b0a-8e04-172d8a04aba2)

<p>

</p>

![image](https://github.com/jtowns14/configure-ad/assets/139197948/9f2ae63b-0c45-46c2-a9d2-455774cc4127)

<p>

</p>
<p>
After connecting to the VMs via Remote Desktop, I began a continuous ping from the Client to the DC to validate connectivity. As the ping requests were not receiving responses, I accessed the Windows Defender Firewall on the DC. Enabling Core Networking Diagnostics for the ICMPv4 protocol within the firewall settings allowed the DC to respond to the ping requests, which were then visible in the command-line interface (CLI).
</p>
<br />


![image](https://github.com/jtowns14/configure-ad/assets/139197948/9ec14bf1-c013-4020-a1cc-eb073636fc5b)

<p>

</p>
<p>

</p>
<p>
In the DC, I installed Active Directory Domain Services (AD DS) from the Server Manager Dashboard. Once AD DS was installed, I promoted the machine to a Domain Controller so that it could manage devices and accounts on the domain.
</p>
<br />

![image](https://github.com/jtowns14/configure-ad/assets/139197948/5ea912e7-2f5b-48ec-a61c-9ec5b81015ce)

<p>


</p>
<p>
Now that Active Directory was all set up, I added two organizational units (OU) and a user. The OUs were _ADMINS and _EMPLOYEES, and the new user was “Jane Doe.” Jane was going to be an administrator, so I created her account inside the _ADMINS OU and added her as a member of Domain Admins. I logged out of the default account that I started with and logged back in as Jane.
</p>
<br />

![image](https://github.com/jtowns14/configure-ad/assets/139197948/29ad3161-7c2b-4aaf-9647-c3a7c96bd6e4)


<p>
  
</p>

![image](https://github.com/jtowns14/configure-ad/assets/139197948/529b5a70-ec45-491d-a0dd-900307ac6bcb)

<p>

</p>
<p>
To continue with setting up my domain, I went back to Azure and set the DC’s private IP address as the DNS server for the Client. After this, I was able to join the Client to my domain. This was confirmed by the “Welcome” box that popped up, confirming that the Client was now part of the domain.
</p>
<br />

![image](https://github.com/jtowns14/configure-ad/assets/139197948/6a11d2cb-6c9b-4469-95d4-f74ce6090f5b)


<p>

</p>
<p>
I enabled Domain Users to user Remote Desktop to access the Client. Remote Desktop is the only way to log into the VM, so enabling this for Domain Users would allow for any user accounts in the domain to be able to log into this machine.
</p>
<br />

![image](https://github.com/jtowns14/configure-ad/assets/139197948/9927ed73-7578-421c-89bb-6129fe1338e6)

<p>

![image](https://github.com/jtowns14/configure-ad/assets/139197948/fe906173-fcbd-4231-9daf-0dfafa2e9c43)

</p>
<p>

</p>
<p>
Lastly, I created 10,000 user accounts using a PowerShell script. All of the accounts were placed into the _EMPLOYEES OU, so I selected a random account and used it to log into the Client. I used the commands “hostname” and “whoami” in the command-line, which confirmed that this was successful.
</p>
<br />

<p>
✨ This lab showed me a lot about how Active Directory works and was really interesting, plus it was cool creating thousands of user accounts using a PowerShell script!
</p>
<br />
