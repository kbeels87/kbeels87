<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Configuring Active Directory in the Cloud (Azure)</h1>
This is a beginners guide that outlines a step by step process of how to deploy Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Creating a Virtual Machine
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

![image](https://github.com/user-attachments/assets/c8a17e87-187e-4f1c-b5df-51e6b374e9ab)


<p>
</p>
<p>
In order to create a virtual machine you must first login to the azure portal and create a new resource group. After this you will need to create a domain controller making sure that your DC is in the same region and to use the appropriate size and image (Winddows Server 2022) or this could cause problems later on. Also you will be required to create a username and password for both your domain controller and your client VM when you log in to remote desktop. After this make sure to put your DC in the right virtual network. After you create your DC you can begin your client VM. You will follow the same steps as before making sure you select the appropriate size, region, and image (Windows 10 Pro). Once the virtual machines are created you will need to set the virtual NIC IP address from private to static. After the VM is created you will need to set the clients DNS settings to the DC private IP address, this will allow us to join the domain. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Next you will want to begin to install Active Directory Domain Services. In order to do this we will need to use remote desktop to login to our Domain controller using the public IP address. Once Active Directory is installed you will be able to configure it to become an actual domain controller in what is called a new forest. Once AD is installed and you have created a new forest you will need to create a domain Admin user within the domain. This will allow the Admin to create new users and be able to reset passwords etc. Once this is completed you will want to join the client user to the domain. 
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
