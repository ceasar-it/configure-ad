<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
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

-Setup on Domain Controller VM (DC-1) and a Client in Azure and set the Domain Controller as the DNS Server

-Install Active Directiory Domain Servies on the Domain Controller VM 

-Create a Domain Admin user within the 

-Join client to the domain 

-Create additional users and attempt to log into client with one of the users.

<h2>Deployment and Configuration Steps</h2>

</p>
<br />

In this lab I create one virtual machine running windows server. This will act as a domain controller. On a serperate virtual machine I setup windows 10 and it acts as a client that will join the domain. 
This client will then be able to login using users that exist on the doamin controller. 

</p>
<br />

Normally the client would find domain name system infromation from the virtual DNS server automatically. In this lab the client is instrtuscted to find DNS information from the domain controller directly.
The client is set to look to our domain controller's IP address for the DNS server.
</p>

![AD VM setup](https://github.com/user-attachments/assets/9e6d0844-8a84-4458-aff1-a817c00efaac)

</p>
<br />

Start by setting up Client vitual machine and domain controller virtual machine in Azure.

![advm](https://github.com/user-attachments/assets/2fc4f8da-8e54-4ba5-a406-eefed020fb18)

</p>

Set the network address for the domain controller and set it as static so that it doesn't change 

![advmdc](https://github.com/user-attachments/assets/94322a32-2e6d-48ca-af9a-d959ad9f73f6)

</p>

Once they are both set up. Use the RDP into the domain controller and turn off all of the firewalls.

![DC Homepage](https://github.com/user-attachments/assets/b3b1fd31-5f52-4f01-873a-56d26a708ef4)

</p>

Next, setup the client-1's DNS settings to the Domain Controller's Private IP Address in Azure. This will ensure that the client pulls domain name system information directly from the domain controller and not a different virtual source. 

![Set DNS of client to private IP of DNS server](https://github.com/user-attachments/assets/6da1991d-b0a7-4524-b893-9b20a04e6bb5)

</p>

Next, log into the Domain Controller VM and install Active Directory Domain Services on the Server manager and promote the server to a domain controller. These are both done on the server manager dashboard 

![Install AD domain servies on DC](https://github.com/user-attachments/assets/4d3b642c-db20-4e3c-aadf-13b8d94e7f80)

</p>

![Promote domain into a AD server](https://github.com/user-attachments/assets/2bfd910c-5528-4b36-a0d1-33c83fca9c59)

</p>

On the DC virtual machine, create a folder for employees and admins. These are called orginizational units. It's created inside of the 
Active Directory Users and Computers folder. 

![Creating Admin-Employees orginizational folder in AD](https://github.com/user-attachments/assets/84df72f4-f6f0-42a1-a0bb-b997998bb963)


</p>

I add a new user that will be setup in the domain controller and will be able to log into the client virtual machine. I name this user Jane Doe and give them administrator privileges. 

![Creating Admin-Employees orginizational folder in AD](https://github.com/user-attachments/assets/e6459406-8748-4aea-94f7-4037b3cd0bf8)

</p>

![Adding new user as admin in AD](https://github.com/user-attachments/assets/d9f249c7-8a85-4322-a7c3-60393f619d54)

</p>

![Setting up Admin properties for new user in AD](https://github.com/user-attachments/assets/68e9b81a-bb19-42b3-a10c-02caf34db7ca)

</p>


Next join the client to the domain controller by making it a member of the domain controller in system settings. 

![Joinng client to DC-1](https://github.com/user-attachments/assets/bd6e4ee0-d147-49c7-96f8-c43052cca4d2)

</p>

Log in to the domain controller from the client using the Jane Doe admin information that was created earlier.

![login to dc from client using jane admin info](https://github.com/user-attachments/assets/424af63a-e5b7-4172-96c0-b67bd1bc1f8a)

</p>

Open Powershell on the virtual machine and run a name gernerating script. Powershell will then create 1,000 random users and add them to active directory users.

</p>

![Open Powershell and Run a name generating script](https://github.com/user-attachments/assets/f92f9418-3c3a-41df-bcb6-7f356e725918)

</p>
![Powershell script creating 1000 of random users](https://github.com/user-attachments/assets/e2f16c96-6023-453f-9543-32113d09dae7)

</p>
![Generated users showing in Active Directory Users and Computers](https://github.com/user-attachments/assets/4880c1ca-34cd-42b8-8a6c-07cfb4b527d7)

</p>



Test the new users by using one of them to log in from the client. 

![Log into client using one of the generated user names](https://github.com/user-attachments/assets/567a5988-d382-42b0-ae6b-3fc9381064ee)









