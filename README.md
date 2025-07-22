<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active-Directory Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Deployment and Configuration Steps</h2>

![AD-3](https://github.com/user-attachments/assets/a0d9fd90-d678-4180-8f29-79366b0cc2d2)



<p>
</p>
<p>
In this lab we will create two VMs in the same VNET. One will be a domain controller, the other will be a Client machine. We will change the DC to a static IP because its offerina Active Directory services to the client machine. Client machine will be joined to the domain. We will control the DNS settings on the client machine, the client machine will use the DC as its DNS server.
</p>
<br />

![AD-11](https://github.com/user-attachments/assets/20852714-0de9-4760-9582-e277c54c104a)


</p>
<p>DC-1 has to have a static IP address. Client one will connect to DC-1 to ensure connectivity we will try to ping DC-1 from Client-1. At first the ping will not work correctly. We have to enable ICMPv4 on the firewall on DC-1. Now we can ping DC-1 successfully from Client-1
</p>
<br />

![AD-12](https://github.com/user-attachments/assets/896e9258-ce8e-45b2-a206-76a8f911d4de)


<p>

</p>
<p>
Next we will begin working on allowing domain users to have access to remote desktop. You can do this by logging into remote desktop with your Admin credentials. When this is finished you should be able to login through your client VM as a non administrative user. After this we will begin to use powershell to create users inside of Active Directory. When you run the script in powershell you should see the user accounts being created. Once the user accounts are finished being created, you can try to login to the Client VM with a random account you have just created.
</p>
<br />

<p>

![ADUC-Reset-Password](https://github.com/user-attachments/assets/0f4101e1-5e0e-419d-99ae-de02a9444b45)



</p>
<p>
Next a common issue that you will be dealing with on the help desk will be unlocking user accounts. We can practice doing this by logging into our domain controller and picking a random user account. Once you do that, log in multiple times with the wrong password using the client VM until you get locked out of the account. Go back to the domain controller and observe that the user is locked out. Unlock the account and attempt to log back in. There are many other things you can do with Group Policy such as resetting passwords and disabling user accounts.
