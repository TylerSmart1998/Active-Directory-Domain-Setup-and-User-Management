<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Active Directory Domain Services

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Install Active Directory
- Create a Domain Admin user within the domain
- Join Client-1 to your domain

<h2>Deployment and Configuration Steps</h2>

<p>


![image](https://github.com/user-attachments/assets/fc027ad0-1247-4c5e-8fa6-0c2c92bc93ab)

</p>
<p>
Login to DC-1 and install Active Directory Domain Services.
Promote as a DC: Setup a new forest as mydomain.com (can be anything, just remember what it is.)
Restart and then log back into DC-1 as user: mydomain.com\labuser

</p>
<br />

<p>


![image](https://github.com/user-attachments/assets/1773d99b-f4c0-4697-bba4-1dab60154813)

In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES.”
Create a new OU named “_ADMINS.”
Create a new employee named “Jane Doe” (same password) with the username of “jane_admin.” 
Add jane_admin to the “Domain Admins” Security Group.
Log out / close the connection to DC-1 and log back in as “mydomain.com\jane_admin.”
Use jane_admin as your admin account from now on.

</p>
<p>
</p>
<br />

<p>


![image](https://github.com/user-attachments/assets/60a24478-ea65-40ac-8031-0539ff5bbafd)


</p>
<p>
From the Azure Portal, set Client-1’s DNS settings to the DC’s Private IP address.
From the Azure Portal, restart Client-1.
Login to Client-1 as the original local admin and join it to the domain (computer will restart.)
Login to the Domain Controller and verify Client-1 shows up in ADUC.
Create a new OU named “_CLIENTS” and drag Client-1 into there.

</p>
<br />
