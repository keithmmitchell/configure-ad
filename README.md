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

- Setup resources in Azure
- Ensure Connectiviity between the client and DC
- Install Active Directory
- Create an Admin and User account in Active Directory
- Join Client1 to the domain
- Setup Remote Desktop for non admin users on Client1
- Create additional users and attempt to log into to Client1

<h2>Deployment and Configuration Steps</h2>

<p>
From the main menu select Virtual Machines to bring up the Virtual Machines blade then select Create An Azure Virtual Machine.
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

- Virtual Machine Name: DC1
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

Create the client machine using the same steps as above with the following configuration:

- Resource Group: AD-Lab
- Virtual Machine Name: Client-1
- Region: (Europe): UK South
- Image: Windows 10 Pro
- Size: Standard_E2s_v3 - 2vcpus, 16GiB memory
- Username: labuser
- Password: Passw0rd1234

Then check the box to confirm licensing and then Next to reach Networking.

<br />



![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/63434afd-83d7-40ec-b55e-4631e90fc318)

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/ec9affbb-c603-46da-b3ff-b184608ec172)

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/f9497f31-511e-484c-a14d-e624caf392b2)

We can confirm the Netowrking settings are okay so we can Review and Create.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/5ec324de-a128-4b94-a565-575adfd5f966)

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/9fca5e03-dd2f-4005-9dc5-51b41bf6df4b)

The next task is to set the DC IP address to static so search Virtual Machines and bring up the DC-1 blade.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/094d1236-9833-4674-b697-ab84784cca55)


Under Networking select Network Settings and click on the Newtork Interface. 

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/d0df426f-897a-4ce9-8cc3-209ad0550a20)

<br/>

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/ec10571d-f039-4010-9996-3cd8232c167b)

In the Network Interface Menu select IP Configurations.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/6f269818-3ea1-4287-9ca1-28f77ad53c82)

From there we can see the IP address is dynamic so click on ipconfig1 and change it to dynamic and Save.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/6a3dd4e8-6af4-4bbc-bdb5-c6ecb5ac0a5e)

<br/>

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/e47701da-e477-4e74-84f6-0159e152de57)

The next task is to ensure connectivity between the DC and Client.  To do that we log into Client-1 and  use the ping -t command which will fail.  If we log into DC-1 and enable ICMPv4 in the local Windows firewall we can then see the pings being sent and received.  

If we go to virtual machines and select Client-1 we can confirm that the public IP address is 172.187.230.132.  

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/59dd5f2e-a628-40e6-b485-77a94d4dde22)


Then on the physical machine search remote destkop for Remote Desktop Connection and enter Client-1's IP address 172.187.230.132 then click Connect.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/a27be6e2-6311-4e7e-9a8d-ff8d0cb4f1eb)

<br />

Select More Choices then enter username labuser and password Passw0rd1234 and click OK to connect.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/96188f45-d3d1-4995-974b-1eb5aad67546)

Click Yes when the message appears about the identity not being verified.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/5bc44a2a-97a1-4abb-b201-56b091311bbc)

Back in Azure we need to confirm the IP address of DC-1.  So back in Virtual Machines select DC-1 and under Networking select Network Settings.  There we can see the private IP address is 10.0.0.4.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/b57ec6df-8606-4091-b94f-a3debe40b613)

Back in Client-1 select Yes to allow the PC to be discoverable by other devices on the network.  Search Powershell and use the command ping -t 10.0.0.4 and we can see it times out.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/91fbdc42-cb23-4dc4-a24c-c71ff2220bf9)

Go back to DC-1 in Azure and we can see the public IP address is 51.11.179.136

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/15117bf8-6936-44e0-ad61-e724f31fd601)

We can then open another instance of Remote Desktop Computer and log into DC-1 using the 51.11.179.136 IP address, the labuser username and Passw0rd1234 password.  Again, select Yes when the identity is not verified.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/24f96568-7ea5-459d-ad3e-1fb7fd4edd93)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/8d245bcb-f26c-43f9-b82f-89939c327586)

<br />

In the Domain Controller search wf.msc to bring up the Firewall and select Inbound Rules

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/4bf93b93-65d6-4343-9610-f0cd1a7c3118)

<br />

Look for the Core Network Diagnostics ICMPv4 rules and right click to enable them.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/be428397-21f0-4c7f-9719-683af415e82b)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/09993623-0e67-44cc-bdc0-1ea21d4dab3c)

If we go back to Client-1 we can now see the pings are successful and press Ctrl+C to stop the pings.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/8150122b-89d1-46cd-b772-c1988596d808)

Now we have connectivity we can install Active Directory from Server Manager on DC-1.  Select Add Roles and Features.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/fae5e83d-e7e1-479f-acb1-616fa39e6e4d)

Click Next.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/2d977134-e943-4e4e-a857-523a14a7398f)

Then Next.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/816baf0f-b288-4210-be2a-c89e47f579e1)

We can see DC-1 is selected then click NExt.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/2101f420-29f9-4f3e-8486-b4419fd81fc7)

From the list select Active Directory Domain Services.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/617dd677-8d22-4a77-8f7b-18645046d8ac)

Then click Add Features.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/b81995f7-d851-44b9-8578-f6965194764e)

Keep clicking Next and then finally Install.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/19595c80-32da-4625-9fe4-747aff4b0654)

Once it's installed click Close.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/74d8661c-911d-4166-b990-590338744503)

The Server still needs to be promoted to a Domain Controller so click on the notification to bring up the blue link to select.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/09f342f0-f599-4fb5-894c-c242d754c72a)

In the Active Directory Domain Services Configuration Wizard select Add A New Forest then enter the Root Domain Name and select Next.  In this lab I have named it mydomain.com.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/b89aac68-3cb2-41bd-8337-eb3f3eecb313)

In the next window enter a password. For this lab I used Passw0rd.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/6c3f273f-32cd-49f1-982c-e2ba05b6a66e)

Keep clicking Next then in Additional Options MYDOMAIN will get poulated for the NetBIOS domain name.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/0e202ac9-2383-4987-9cb5-db1955e6c475)

Once all the prerequisites have been checked click on Install.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/f0e172d5-8477-4a87-a44f-270c072c9d7b)

Once it has installed the connection is disconnected and need to reconnect throught Remote Desktop.  Since it is now part of the domain I need to login in with the Fully Qualified Domain Name mydomain.com\labuser.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/846f17bf-788b-4fbc-a508-2fdf69a6484b)

Next I'll create some Organisational Units and an Administritive User.  To do this start by clicking Tools then select Active Directory Users and Computers.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/923c6fcf-0ca3-4699-928e-2f49f68e214c)

We will now create two Organisational Units by right clicking Mydomain.com>New>Organisational Unit and calling one _EMPLOYEES and the other _ADMMINS.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/eac4d157-9891-47d9-8446-abb1a566570c)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/f6f12055-0342-4e8b-8fde-171450710241)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/b53d4321-10df-4d15-96d2-402f40e4d636)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/cb0a4d80-3217-499f-8784-6b97a6ff2099) 

We will now create a new Admin account by clicking the _ADMINS Organisational Unit then right clicking New>User and we will call the user Jane Doe with a User Logon Name of jane_admin then click Next.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/37d34d69-7a97-4bf1-9ead-c482a7d14443)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/940a2385-45bd-4784-98ea-4eb0812dd9d0)

Enter a password.  In this lab I used Passw0rd then unchecked password must be changed at next logon and checked password never expires then click Next then Finish.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/18ab6cb7-8eec-4e1f-95a3-6f08b48a81ee)

We now need to make this an Admin account by assigning it to the Domain Admins group.  We do this by right clicking it and selecting Properties.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/6fc91c93-56db-4c21-b6f3-86b5a4bd9bef)

In the Member Of tab we click Add.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/880b1a43-9015-48c9-a3b5-aaf42a5d4176)

In Select Groups enter domain then click Check Names then select Domain Admins.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/02ffd4c6-1932-46d1-9a4f-666faebb4eb3)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/034a31c5-05f5-4a92-961f-ec8f83719ee2)

Keep cicking OK for Jane Doe to be a member of Domain Admins.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/d6d22727-e1cb-4239-ae34-a711cde03671)

Now I Logout, close the Remote Desktop Connection and log back in as mydomain.com\jane_admin. 

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/e0c8019e-c997-4cd7-8a8d-69bf294c61b7)

Next is to joine Client-1 to the domain.  First is to set Client-1's DNS settings to the DC's private IP address from Azure Portal.

We can see the private IP address of DC-1 is 10.0.0.4.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/35191295-fba8-46e6-9dbd-53ef981996f0)

In Azure, select Client-1 then Network Settings.  From there the NIC can be selected.  Here it is client-1104_z1.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/4b9e36c0-0745-4244-98d0-e2f1dd64dd08)

Then select DNS Servers.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/b9e9222c-52d7-4f95-a190-031f662f15ba)

Select Custom, enter 10.0.0.4 then click Save.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/36d86de5-89f4-4935-a9b1-df2c69d5a029)

Next Client-1 needs to be restarted to flush the DNS cache.  Back at Client-1 select Restart.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/88df70d6-53af-4d07-a94d-dacac1f43b05)

We now need to log back in as labuser because it's not joined to the domain.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/e22ed187-3f2c-4f5e-9551-043a690e22cf)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/0b1d436b-68e1-4432-8a6b-bc4cb780d79c)

Enter command prompt and type ipconfig/all to inspect the DNS settings and see DC-1's IP address 10.0.0.4.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/920129d6-4d46-4825-989f-7da6bf66fd59)

Now to connect Client-1 to the domain go into Settings, select About then Rename this PC (Advanced) 

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/8d9ecb4f-eb6c-4b29-854a-d5423fac39f7)

Then Change to change it's domain or workgroup

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/886d235b-076f-4385-a5dd-7722aabc93c3)

Select Domain then entermydomain.com

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/3781941b-f369-44a8-b5d6-377a85b94301)

We are then prompted to enter the credentials of an account with permission to join the domain.  Enter mydomain.com\jane_admin and Passw0rd then click OK.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/61c9ea28-69e2-432e-b273-1d9301554bf1)

We can now see the dialog box welcoming us to the domain.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/1682bd0a-7974-46e6-9dca-ac7eb5006fdd)

Client-1 now needs to be restarted so restart now.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/a9f959fe-b857-4eaa-ab56-0ba6b0e51d17)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/7b5507a5-e2db-4613-9d98-1e542a2d28c0)

Log back into Client-1 but this time use the Jane_Admin credentials to log into the domain.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/840bcb18-f950-47c9-990e-3cd030a98462)

Go to System Properties, Remote Desktop then under Use Accounts click Select users that can remotely access this PC.

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/0b1568b1-8297-4040-b1e3-34a2543559bb)

Click Add

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/ea9e0bd8-b433-4096-8130-76e43bd9256d)

Then instead of adding individual users enter domain users for the Domain Users group then click Check Names.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/375bc04c-6789-49ff-b7d7-1610c4e37880)

Click OK and we can see the group has been added and click OK.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/15aaaf44-5f54-4ead-ad31-962926b8745a)

In DC-1 go back to Active Directory Users and Computers

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/1f9aab14-036e-4caf-a2a6-ccba1aca0dcb)

In users under mydomain.com we can see the Domain Users group and by right clicking and selecting Properties we can see the members of that group. 

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/3311f739-ce00-4bd2-969b-deeb427c81ea)

Now I create additional users and attempt to log into Client-1 with one of them.  I do that by opening Powershell_ise as an administrator in DC-1.  

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/bb920ff7-7db9-4bac-9e0e-1c7d16568a83)

Inside Powershell open a new file and enter the following script:

 # ----- Edit these Variables for your own Use Case ----- #
$PASSWORD_FOR_USERS   = "Password1"
$NUMBER_OF_ACCOUNTS_TO_CREATE = 10000
# ------------------------------------------------------ #

Function generate-random-name() {
    $consonants = @('b','c','d','f','g','h','j','k','l','m','n','p','q','r','s','t','v','w','x','z')
    $vowels = @('a','e','i','o','u','y')
    $nameLength = Get-Random -Minimum 3 -Maximum 7
    $count = 0
    $name = ""

    while ($count -lt $nameLength) {
        if ($($count % 2) -eq 0) {
            $name += $consonants[$(Get-Random -Minimum 0 -Maximum $($consonants.Count - 1))]
        }
        else {
            $name += $vowels[$(Get-Random -Minimum 0 -Maximum $($vowels.Count - 1))]
        }
        $count++
    }

    return $name

}

$count = 1
while ($count -lt $NUMBER_OF_ACCOUNTS_TO_CREATE) {
    $fisrtName = generate-random-name
    $lastName = generate-random-name
    $username = $fisrtName + '.' + $lastName
    $password = ConvertTo-SecureString $PASSWORD_FOR_USERS -AsPlainText -Force

    Write-Host "Creating user: $($username)" -BackgroundColor Black -ForegroundColor Cyan
    
    New-AdUser -AccountPassword $password `
               -GivenName $firstName `
               -Surname $lastName `
               -DisplayName $username `
               -Name $username `
               -EmployeeID $username `
               -PasswordNeverExpires $true `
               -Path "ou=_EMPLOYEES,$(([ADSI]`"").distinguishedName)" `
               -Enabled $true
    $count++
}

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/8e9f1e5d-382c-410c-8e34-ce97609a2d0e)

Run the script, by either pressing F5 or the green arrow, and observe the accounts being created. 10,000 accounts will be created with the password "Password1" in the _EMPLOYEES Organisational Unit.  Back in Active Directory Users And Computers we can see in accounts in the _EMPLOYEES OU

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/fc636516-7c0c-459f-a965-a9860dd067a3)

Back in Client-1 sign out as jane_admin then in Remote Desktop log in using one of the newly created accounts. 

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/77f82d61-00e3-49d0-b250-6ef7f576719b)

We can see in the command prompt in Client-1 we are logged in as the beg.bir account.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/40975d4c-60b5-4df3-b53f-de6bccabe9e0)

Back in DC-1 we can see if we right click a username then select Properties we can go to the Accounts tab.  We can see the account can be unlocked from there if it ever becomes locked.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/5972bd9f-51ed-4619-9119-232c65e633e4)

Also by right clicking then name we can change the password and unlock from there as well if required.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/d94b5d16-7cce-4eb2-b65f-1cbe2efc5397)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/25286930-c2ec-4420-bfbb-355c65f568bc)

Next I will demonstrate file share permissions.  

On DC1 I will create four folders on the c:\ drive "read access", "write access", "no access" and "accounting".

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/3a562fb4-7cdd-4aaf-9ec5-8fbba3a716d9)

The following permissions will be set:

- Folder: "Read Access", Group: "Domain Users", Permission: "Read"
- Folder: "Write Access", Group: "Domain Users", Permission: "Read/Write"
- Folder: "No Access", Group: "Domain Admins", Permission: "Read/Write"

Right click the Read Access folder and select Properties then the Sharing tab then Share.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/ab91d681-be4e-46f3-bab6-1f20407e2ca1)

Type domain users then click Add

<br/>

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/1990da2f-b9ec-4295-b725-9dbb22585635)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/867b0e02-b957-4c26-9de6-f7a424f11ab9)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/b755be48-0e08-4b42-9b7c-4ba5e763a797)

Then give the Write Access folder Write Access.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/815800da-de51-4058-a2d4-ba8bfcfda5e7)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/da67ffb8-f0ac-4144-8db2-a43e750e4e2c)

For the No Access folder give the Domain Admins the "Read/Write" permissions so standard users won't have access.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/b8ff5557-33a2-4bcd-9730-f6124c522364)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/435e049b-2fbe-4c5d-9d18-4af90a057011)

On Client-1 navigate to the shared folders by going to File Explorer and enter \\DC1 in the address bar then Return.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/95c78dc5-7632-4f06-a8e0-7c2176578bea)

If I try to access the NO Access folder I get the dialog saying I don't have permission.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/b46ef64e-e5a5-496e-86be-ffb3690273a5)

If I open the Read Access folder then right click and select New>Text Document I get a dialog saying access is denied because I need permission.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/2ef80865-40bb-45ba-998b-94a1869750ff)

If there is a file in the Read Access folder then I can open it to read.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/928f76e9-c52f-493e-8903-e9b44b01351e)

If I open the Write Access folder then right click and select New>Text Document then the document is created.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/5cbcf176-b7a3-4ce7-a6de-130af1251c06)

Now on DC1 create Security Groups OU and an Accountants group then configure Read and Write permissions for the "Accounting" folder.  Back in Active Directory Users and Computers right click mydomain to create the OU.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/cd7e06dc-bdab-448f-b957-def7d7405cd8)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/187d0068-46e0-46cd-a979-1ab43c6c9bfe)

In the _SECURITY_GROUP right click and select New>Group

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/a4f9afae-e02b-440f-94d4-9181d0e1f003)

In the New Object - Group window enter ACCOUNTANTS and click OK.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/4e3cba7f-dedd-4cd8-b3aa-65a62cdd4304)

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/4afb5e3f-7717-43b7-9c19-bde946c9d41d)

Go back to the C:\ drive and right click the Accounting folder, select Properties then the Sharing tab then select Share.  Add the ACCOUNTANTS group and give it Read and Write permissions.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/edca0b8e-838e-4fab-8a85-2e0ca473c9fb)

Back in Client-1 I can try and access the folder using the beg.bir account and get a message saying that access is denied.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/f222d605-32dc-422c-bedc-d27c2def7cfa)

If I go back to DC1 and add beg.bir to the ACCOUNTANTS group I will then have access.

In the ACCOUNTANTS group in Active Directory Users and Computers, right click and select Properties.  Click on the Memebers tab and select Add.  From there enter the name beg.bir and click OK.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/762d9119-5185-4602-bd82-91a8c36e32e7)

For the new permissions to work on Client-1 I need to logout then log back in again as beg.bir and will have access to the accounting folder.

<br />

![image](https://github.com/keithmmitchell/configure-ad/assets/174253055/5eacd608-84a4-490d-8f55-0030e2e89b15)

That brings us to the end of this lab.


