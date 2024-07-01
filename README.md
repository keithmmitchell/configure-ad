<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup resources in Azure
- Ensure Connectiviity between the client and DC
- Install Active Directory
- Create an Admin and User account in Active Directory
- Join Client1 to the domain
- Setup Remote Desktop for non admin users on Client1
- Create additional users and attempt to log into to Client1

<h2>Deployment and Configuration Steps</h2>

<p>
From the main menu select Virtual Machines to bring up the Virtual Mchines blade then select Create An Azure Virtual Machine.
</p>
<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/1814e180-87ca-4b91-ab3b-f3f318f28d12)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/a47dd005-4c6c-459c-9a3c-c35289b6d7bb)


<p>
Select Create New under Resource Group and give it a name then click OK.  I have called it AD-LAb.
</p>

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/6123ce69-6af1-44ae-b55b-0b67857a68cf)

Enter the following configuration:

- Virtual MAchine Name: DC1
- Region (Europe) UK South
- Image: Windows Server 2022 Datacenter
- Size: Standard_E2s_v3 - 2vcpus, 16GiB memory
- Username: labuser
- Password: Passw0rd1234

Then click Review + Create.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/b8eaf705-164f-4dbc-b415-00f47e52d51a)

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/ad3546bf-c216-4ae0-bb51-4dff34b286c5)

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/296542d1-ff87-4065-be7c-72abfb1be3ca)

Once the validation is passed click Create.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/65fc12d9-7ee0-4f89-a522-c6af71a6b604)

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/ab2fc7d6-289e-411b-8194-d10c199d483c)





