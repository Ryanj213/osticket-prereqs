**# osticket-prereqs*<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Item 1 (Create Virtual Machine in Azure)

![image](https://github.com/Ryanj213/osticket-prereqs/assets/157759490/ff12b6d9-16e9-4ffa-bf35-4a8d47381ed1)

Create a Resource Group
Create a Windows 10 Virtual Machine (VM) with 2-4 Virtual CPUs
When creating the VM, allow it to create a new Virtual Network (Vnet)

- Item 2 Create an Azure Virtual Machine Windows 10, 4 vCPUs
Name: Vm-osticket
Username: labuser (for example/whatever you chose)
Password: osTicketPassword1! (for example/whatever you chose)



Open this: Installation Files
We will use these files to install osTicket and some of the dependencies. I’m using this offline version to make sure everyone is using the same version of all the files :)

Install / Enable IIS in Windows WITH
CGI and Common HTTP Features
World Wide Web Services -> Application Development Features ->
[X] CGI
[X] Common HTTP Features
AND IIS Management Console
Internet Information Services -> Web Management Tools -> IIS Management Console
	[X] IIS Management Console


From the Installation Files, download and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)

From the Installation Files, download and install the Rewrite Module (rewrite_amd64_en-US.msi)

Create the directory C:\PHP

From the Installation Files, download PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) and unzip the contents into C:\PHP
!! ATTENTION !!
If this appears, choose to “Keep” the file: 

From the Installation Files, download and install VC_redist.x86.exe.

From the Installation Files, download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi)
Typical Setup ->
Launch Configuration Wizard (after install) ->
Standard Configuration ->
Password1

Open IIS as an Admin

Register PHP from within IIS

Reload IIS (Open IIS, Stop and Start the server)

Install osTicket v1.15.8
Download osTicket from the Installation Files Folder
Extract and copy “upload” folder to c:\inetpub\wwwroot
Within c:\inetpub\wwwroot, Rename “upload” to “osTicket”

Reload IIS (Open IIS, Stop and Start the server)

Go to sites -> Default -> osTicket
On the right, click “Browse *:80”

Note that some extensions are not enabled
Go back to IIS, sites -> Default -> osTicket
Double-click PHP Manager
Click “Enable or disable an extension”
Enable: php_imap.dll
Enable: php_intl.dll
Enable: php_opcache.dll
Refresh the osTicket site in your browse, observe the changes

![image](https://github.com/Ryanj213/osticket-prereqs/assets/157759490/daa88f9b-10bf-4c56-a32c-0fec2ffb04db)


Rename: ost-config.php
From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php
To: C:\inetpub\wwwroot\osTicket\include\ost-config.php

Assign Permissions: ost-config.php
Disable inheritance -> Remove All
New Permissions -> Everyone -> All

![image](https://github.com/Ryanj213/osticket-prereqs/assets/157759490/9f02c186-93d7-48f9-ab38-34f8af0d08b5)

Continue Setting up osTicket in the browser (click Continue)
Name Helpdesk
Default email (receives email from customers)

From the Installation Files, download and install HeidiSQL.
Open Heidi SQL
Create a new session, root/Password1
Connect to the session
Create a database called “osTicket”

![image](https://github.com/Ryanj213/osticket-prereqs/assets/157759490/750ccaf8-63a7-49d0-80a3-1c9d47364f4c)

Continue Setting up osticket in the browser
MySQL Database: osTicket
MySQL Username: root
MySQL Password: Password1
Click “Install Now!”

Clean up
Delete: C:\inetpub\wwwroot\osTicket\setup
Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php

![image](https://github.com/Ryanj213/osticket-prereqs/assets/157759490/69a18c35-340b-46c5-aee8-60f7a1e8a2a4)

- Item 3 (Post Installation Setup)
  
Configure Roles
Admin Panel -> Agents -> Roles
Supreme Admin
Configure Departments
Admin Panel -> Agents -> Departments
System Administrators

Configure Teams
Admin Panel -> Agents -> Teams
Level I Support
Level II Support
Allow anyone to create tickets
Admin Panel -> Settings -> User Settings
Registration Required: Require registration and login to create tickets 
Configure Agents (workers)
Admin Panel -> Agents -> Add New
Jane
John

Configure Users (customers)
Agent Panel -> Users -> Add New
Karen
Ken

Configure SLA
Admin Panel -> Manage -> SLA
Sev-A (1 hour, 24/7)
Sev-B (4 hours, 24/7)
Sev-C (8 hours, business hours) Configure Help Topics Admin Panel -> Manage -> Help Topics Business Critical Outage Personal Computer Issues Equipment Request Password Reset

- Item 4 (Tickets and Ticket Lifecycle)

Just practice creating, triaging, and solving tickets. I recommend watching videos to learn about triaging multiple tickets.

Ticket examples:
Sev-A (1 hour, 24/7) [entire mobile/online banking system is down] -> SysAdmins
Sev-B (4 hours, 24/7) [accounting department needs adobe upgrade, broken]
Sev-B/C (2 hours, business hours) [CFO’s laptop seems a bit slow]
