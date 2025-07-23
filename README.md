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




<p>
</p>
<p>
In this lab we will create two VMs in the same VNET. One will be a Domain Controller, the other will be a Client machine. We will change the DC to a static IP because its offering Active Directory services to the client machine. Client machine will be joined to the domain. We will control the DNS settings on the client machine, the client machine will use the DC as its DNS server.
</p>
<br />

<img width="1004" height="858" alt="image" src="https://github.com/user-attachments/assets/85fdf9a2-4a4f-441c-adb0-ba5a2569a10e" />


</p>
DC-1 has to have a static Private IP Address. Client one will connect to DC-1 to ensure connectivity we will try to ping DC-1 from Client-1. At first the ping will not work correctly. We have to enable ICMPv4 on the firewall on DC-1. Now we can ping DC-1 successfully from Client-1
</p>
<br />

<img width="1044" height="781" alt="image" src="https://github.com/user-attachments/assets/133269d3-9734-4693-af1c-0a45452f2e54" />


<img width="977" height="510" alt="image" src="https://github.com/user-attachments/assets/dae3395a-32ea-4ce4-8fae-33c1e059a1db" />



<p>

</p>
<p>
Now we will log back into DC-1 to install AD Users & Computers. Promote the VM to DC, setup a new forest as "mydomain.com" afterwards restart then log back into DC-1 as user: "mydomain.com\labuser". If you performed the steps properly you should be able to run AD Users & Computers as shown below.
</p>
<br />

<p>

<img width="752" height="528" alt="image" src="https://github.com/user-attachments/assets/9ad4cd87-3fb1-472f-a966-62025c2123a1" />




</p>
<p>
We can start creating Organizational Units (OU). Let's first create an OU named _EMPLOYEES. Create another OU named _ADMINS. In order to do that right click on the domain area. Select new->Organizational Unit and fill out the field. Then click inside of your OU and right click, select new and select user and fill out the information for your new user. The user should be named Jane Doe, she is going to be an Admin so her username will be Jane_admin. Lastly add Jane to the domain admins security group.

<img width="1616" height="574" alt="image" src="https://github.com/user-attachments/assets/3d3347cb-bb6a-4332-b18e-2a982bf16a4f" />


<img width="589" height="308" alt="image" src="https://github.com/user-attachments/assets/26be3b1b-fa2c-401b-b402-c54ce5730afd" />



From now on you can use Jane_admin as the administrator account. Now we will join Client-1 to the domain (mydomain.com) from the azure portal we will change client-1's DNS settings to the DC's Private IP address. After you do that restart Client-1 from within the Azure portal. Our picture below shows verification that client-1 is on the DC-1 DNS.

<img width="1083" height="542" alt="image" src="https://github.com/user-attachments/assets/17043033-6b50-432b-8a1a-71d4fadd3552" />

<img width="976" height="512" alt="image" src="https://github.com/user-attachments/assets/4a09cb25-fea0-4d54-92f9-7a9a17059d90" />


We have to join Client-1 to the domain in order to do so navigate to your system settings and go to about. Off to the right select rename this pc (advanced). From there select to change the domain. Enter "mydomain.com" after that enter your credentials from mydomain.com\labuser. Your computer will restart and then client-1 will be a part of mydomain.com

<img width="1195" height="762" alt="image" src="https://github.com/user-attachments/assets/911fe02e-b49d-4cab-bbec-56653e3f08db" />



Client-1 is now a part of the domain. Now we will set up remote desktop for non-administrative users on Client-1. We have to log into Client-1 as an admin and open system properties. Click on "Remote Desktop", allow "domain users" access to remote desktop. After completing those steps you should be able to log into Client-1 as a normal user.


<img width="857" height="661" alt="image" src="https://github.com/user-attachments/assets/259ef5c5-4f79-4993-948a-5a8200e0b20f" />


Lastly to verify that noraml users can RDP into Client-1 we will use a script to generate thousands of users into the domain. We will input the script in powershell, after the users are created we will select one and RDP into Client-1.

<img width="1432" height="978" alt="image" src="https://github.com/user-attachments/assets/77ca5976-c1e2-419a-9ac3-579f2b24bc3c" />

<img width="397" height="452" alt="image" src="https://github.com/user-attachments/assets/b2065e92-21d9-476a-856c-354d4bee50d7" />

<img width="546" height="223" alt="image" src="https://github.com/user-attachments/assets/0bb31f99-7704-46e9-8a57-217257e5e2c8" />




As you can see the Powershell script created a user with the username "bab.hubo" We were able to login to Client-1 with his credentials as a normal user.
