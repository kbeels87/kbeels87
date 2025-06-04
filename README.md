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
- Installing Active Directory Domain Services
- Using Remote Desktop / Powershell
- Configuring Group Policy

<h2>Deployment and Configuration Steps</h2>

![AD-3](https://github.com/user-attachments/assets/a0d9fd90-d678-4180-8f29-79366b0cc2d2)



<p>
</p>
<p>
In order to create a virtual machine you must first login to the azure portal and create a new resource group. After this you will need to create a domain controller making sure that your DC is in the same region and to use the appropriate size and image (Winddows Server 2022) or this could cause problems later on. Also you will be required to create a username and password for both your domain controller and your client VM when you log in to remote desktop. After this make sure to put your DC in the right virtual network. After you create your DC you can begin your client VM. You will follow the same steps as before making sure you select the appropriate size, region, and image (Windows 10 Pro). Once the virtual machines are created you will need to set the virtual NIC IP address from private to static. After the VM is created you will need to set the clients DNS settings to the DC private IP address, this will allow us to join the domain. 
</p>
<br />

![AD-11](https://github.com/user-attachments/assets/20852714-0de9-4760-9582-e277c54c104a)


</p>
<p>
Next you will want to begin to install Active Directory Domain Services. In order to do this we will need to use remote desktop to login to our Domain controller using the public IP address. Once Active Directory is installed you will be able to configure it to become an actual domain controller in what is called a new forest. Once AD is installed and you have created a new forest you will need to create a domain Admin user within the domain. This will allow the Admin to create new users and be able to reset passwords etc. Once this is completed you will want to join the client user to the domain. 
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
Next a common issue that you will be dealing with on the help desk will be unlocking user accounts. We can practice doing this by logging into out domain controller and picking a random user account. Once you do that, log in multiple times with the wrong password using the client VM until you get locked out of the account. Go back to the domain controller and observe that the user is locked out. Unlock the account and attempt to log in with the user and the account should be unlocked. There are many other things you can do with Group Policy such as resetting passwords and disabling user accounts. 
