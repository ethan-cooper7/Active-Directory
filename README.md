# Active-Directory

## Objective

The primary focus of the Active Directory project was to provide an in-depth, hands-on experience with Active Directory and general Windows networking as well as the fundmentals of AAA.

### Skills Learned

- Creating a domain controller that houses Active Directory.
- Hands-on experience creating and configuring Domain/AD DS, RAS/NAT, and DHCP.
- Troubleshooting errors with DNS configuration.
- Utilizing an automation script in PowerShell.
- Successfully joining a client account to a domain.

### Tools Used

- VirtualBox for creation of virtual machines.
- Windows 10 to create a client user that can conect through a DHCP.
- Windows Server to host Active Directory.
- Active Directory to manage authentication, authorization, and accounting (AAA)
- Powershell to run a script that generates 1000 new users.

## Steps
##### Prerequisites
- [Install VirtualBox](https://www.virtualbox.org/)
- [Download Windows 10 ISO](https://www.microsoft.com/en-us/software-download/windows10)
- [Download Windows Server 2019 ISO](https://www.microsoft.com/en-us/evalcenter/download-windows-server-2019)

#

#### Step 1:
- Create a machine using the WIndows Server 2019 ISO.
- Name is "DC" for Domain Controller.

(*Make sure you select the "Desktop Experience" or you won't have a GUI*)

![Step 1](https://github.com/user-attachments/assets/686dc868-cc38-4d27-aedf-95755bf0e217)

#### Step 2:
- Once created, go to "Settings", then "Network".

(*If it immediately boots up, power it off then go into Settings*)

#### Step 3:
- Click "Adapter 2" and add an Internal Network.

#### Step 4:
- Run the Windows Server virtual machine.

#### Step 5:
- Upon the initial Windows setup, create an admin password.

(*For simplicity, I used "Password1"*)

#

##### Quick Note
- We have two NICs
  - **Internet:** will get addressing from home router (**DHCP**)
  - **Internal:** must be setup manually (*see below*)
#

#### Step 6:
- Click the Network Icon in the bottom right of taskbar and select "Network & Internet settings".

![Step 6](https://github.com/user-attachments/assets/9b88e222-e2f1-4c45-a9d8-11f57420faf4)

#### Step 7:
- Click "Change adapter options".

#### Step 8:
*We must find the internal network*

- Right-click either "Ethernet" 1 or "Ethernet 2".

#### Step 9:
- Click "Details" to check for a "169.254..." address.

(*Internal adapter failed to find an IP so it was automatically assigned this*)

![Step 9](https://github.com/user-attachments/assets/97000266-58a9-415f-b8e4-a25af3c783ee)

#### Step 10:
  - Once found, rename the home ethernet to "INTERNET" and the internal ethernet to "internal".

![Step 10](https://github.com/user-attachments/assets/de63084c-e009-4afe-9cc0-eaea258a5ff9)

#### Step 11:
- Right-click on "Internal" and select "Properties".

#### Step 12:
- Double-click "Internet Protocol Version 4 (TCP/IPv4)".

![Step 11](https://github.com/user-attachments/assets/eb1681bf-ef0d-4acb-8e41-ef9eee6aefe8)

#### Step 13:
*Enter the following*

- **IP address:** 172.16.0.1
- **Subnet mask:** 255.255.255.0
- **Prefered DNS server:** 127.0.0.1 (loopback address)

![Step 13](https://github.com/user-attachments/assets/5f579f59-2cdc-40e8-b250-0da7b9eb1ed8)

#### Step 14:
- Open the Server Manager Dashboard.

(*The tab that automatically opens when you run the virtual machine*)

#### Step 15:
- Click "Add roles and features".

![Step 15](https://github.com/user-attachments/assets/09ab4b3b-d937-407e-a118-720001f09997)

#### Step 16:
- Click "Next" until you reach the "Server Roles" tab, then select "Active Directory Domain Service".

![Step 16](https://github.com/user-attachments/assets/aca3169d-3ada-4a05-9af8-ba2ca9980e0e)

#### Step 17:
- Click "Next until you can reach the end, then click "Install".

![Step 17](https://github.com/user-attachments/assets/aec5058a-75bd-4e3a-ba7b-c65d600d48d6)

#### Step 18:
- Afterwards, on the dashboard, click on the flag icon in the top right.

![Step 18](https://github.com/user-attachments/assets/674dafdd-ba99-4fdf-9135-d87ed503f526)

#### Step 19:
- Under "Post-deployment Configuration", click "Promote this server to a domain controller".

#### Step 20:
- Select "Add a new forest", then give it a root domain name and click "Next".

(*For simplicity, I used "mydomain.com"*)

![Step 20](https://github.com/user-attachments/assets/9f4c1b00-1e60-4bc5-bc00-81162a699e90)

#### Step 21:
- On "Domain Controller Options", create a password, then click "Next".

(*It will not be used, so make it simple*)

#### Step 22:
- If "Create DNS delegation" is checked, uncheck it then click "Next".

#### Step 23:
- Click "Next until you can reach the end, then click "Install".

![Step 23](https://github.com/user-attachments/assets/5e581395-1ce7-46d7-9c16-d8c0a0a7b106)

#### Step 24:
- After installation, hit the Start button, click "Windows Administrative Tools".

![Step 24](https://github.com/user-attachments/assets/48e1d66d-2f6a-4da4-89be-a4e371fedd80)

#### Step 25:
- Open "Active Directory Users and Computers".

#### Step 26:
- Right-click "mydomain.com", select "New", then "Organizational Unit".

![Step 26](https://github.com/user-attachments/assets/f1ce6f8a-c344-4826-bc1a-9201d77bdaf5)

#### Step 27:
- Name it "ADMINS" and uncheck "Protect container from accidental deletion".

![Step 27](https://github.com/user-attachments/assets/be96f6c8-e249-4816-adf6-1c0e7fd3dfc6)

#### Step 28:
- Right-click "ADMINS", select "New", then "User".

#### Step 29:
(*Fill out the information with the below format*)

![Step 29](https://github.com/user-attachments/assets/242e77c4-75ee-40b6-8942-b50d06f8879e)

#### Step 30:
- Create a password, check "Password never expires", click "Next" then click "Finish".

![Step 30](https://github.com/user-attachments/assets/7c2b54ec-741b-4f60-9287-be9fe2e5e40f)

#### Step 31:
- Right-click on the new User, and click "Properties".

#### Step 32:
- Click "Member Of", then click "Add".

![Step 32](https://github.com/user-attachments/assets/b9b4313e-0f20-456d-997b-68e2d444bcb4)

#### Step 33:
- In the bottom field, type "domain admins", click "Check Names", click "Ok".

![Step 33](https://github.com/user-attachments/assets/4463b1b2-007f-49d6-9acb-b7e27f6e580d)

#### Step 34:
- Click "Apply".

#### Step 35:
- Hit the Start button and log out.

#### Step 36:
- On the login screen, select "Other User", then enter the new user information.

(*From Steps 29 & 30*)

![Step 36](https://github.com/user-attachments/assets/fa314b43-62c5-4fd1-825a-d93a931ba444)

#### Step 37:
- Once logged in and on the server dashboard, click "Add roles and features".

#### Step 38:
- Click "Next" until on "Server Roles", then select "Remote Access".

![Step 38](https://github.com/user-attachments/assets/2068888c-0e73-403a-94a1-d6b65963548a)

#### Step 39:
- Click "Next" until on "Role Services", then select "Routing".

(*Selecting "Routing" automatically selects "DirectAccess and VPN (RAS)"*)

![Step 39](https://github.com/user-attachments/assets/c5b43dbd-92aa-47fa-b344-a354ce22f270)

#### Step 40:
- Click "Next until you can reach the end, then click "Install".

#### Step 41:
- On the top right of the dashboard, click "Tools", then click "Routing and Remote Access".

![Step 41](https://github.com/user-attachments/assets/78897f52-3716-4327-8f25-d8147192a765)

#### Step 42:
- Right-click on your device (e.g. DC1) and select "Configure and Enable Routing and Remote Access". 

![Step 42](https://github.com/user-attachments/assets/8f9b3eac-0bbb-4dd1-9a91-71625f37f947)

#### Step 43:
- Select "Network address translation (NAT), then click "Next".

![Step 43](https://github.com/user-attachments/assets/2bc60da3-3bb3-4100-855d-fe16b1de5f26)

#### Step 44:
- Select "INTERNET", then click "Next" until you reach "Finish".

(*Selection option may be unavailable. Just close and repeat Steps 41-44*).

![Step 44](https://github.com/user-attachments/assets/f8eb046a-629a-415f-a108-960ff042558b)

#

##### Quick Note
- We have now successfully finished configuration of Domain/AD DS & RAS/NAT
  - Now we must setup a DHCP server on our server
  - This will allow our Windows 10 clients to get an IP address

#

#### Step 45:
- On the dashboard, click "Add roles and features".

#### Step 46:
- Click "Next" until on "Server Roles", select "DHCP Server".

![Step 46](https://github.com/user-attachments/assets/8fc6d98b-6855-4a7f-b4df-a4212b3b764d)

#### Step 47:
- Click "Next" until then end, then click "Install".

#### Step 48:
- On the top right of the dashboard, click "Tools", then click "DHCP".

![Step 48](https://github.com/user-attachments/assets/918c9221-a0bb-4eb3-977a-9176929f01f2)

#### Step 49:
- Click on your DHCP server, right-click "IPv4", then click "New Scope".

#### Step 50:
- Name the scope after the IP range, then click "Next".

![Step 50](https://github.com/user-attachments/assets/3aae21d1-9fad-44a2-af6d-ae6fa29f1a30)

#### Step 51:
*Enter the following:*

![Step 51](https://github.com/user-attachments/assets/50bcdab8-e78e-4d33-a7f8-f138304ddd0d)

#### Step 52:
- Click "Next" until on "Router (Default Gateway).

#### Step 53:
- Type "172.16.0.1", then click "Add".

  *(This is the internal NIC IP)*

![Step 53](https://github.com/user-attachments/assets/958d1810-a55a-47a8-81e5-fc4da2485bc8)

#### Step 54:
- Click "Next" until then end, then click "Finish".

#### Step 55:
- Right-click your DHCP server, click "Authorize, right-click again, then click "Refresh".

![Step 55](https://github.com/user-attachments/assets/5a042365-a130-4aa9-b3b6-d4b84ccd2a31)

#

##### Quick Note *(almost finished!)*
- Now, it's time to have some fun with PowerShell!
- We will run a script to generate 1000 new users.
- Download the files in the virtual machine and put them on your desktop.

[Download Here](https://github.com/joshmadakor1/AD_PS?search=1)
#

#### Step 56:
- Open the "names.txt" file, add your (or any unqiue) name, then save.

![Step 56](https://github.com/user-attachments/assets/c023983c-a28c-4fd3-bc0b-54e8848916d1)

#### Step 57:
- Hit the start button and open PowerShell as an administrator.

#### Step 58:
- Open the "1_CREATE_USERS.ps1" file.

#### Step 59:
- Type "Set-ExecutionPolicy Unrestricted", hit enter, then click "Yes to All".

![Step 59](https://github.com/user-attachments/assets/eab19a5f-8bab-4f99-b077-206e7c6952f3)

#### Step 60:
- Type "cd c:\users\ (username)\desktop\AD_PS-master", then hit enter.

*(This changes directories to the script file)*

![Step 60](https://github.com/user-attachments/assets/87364ef0-1bbb-4451-9b33-6c45e0c56c2a)

#### Step 61:
- Click the green Play icon on the nav bar to run the script.

#### Step 62:
- Hit the Start button, click "Windows Administrative Tools", then open "Active Directory Users and Computers".

#### Step 63:
- Right-click your domain (e.g. mydomain.com) and click "Refresh".

#### Step 64:
- Click "_USERS" to view your brand new minion army!

![Step 64](https://github.com/user-attachments/assets/df89611c-95ab-4da9-bdc2-8974f3b1af4c)

#### Step 65:
- While leaving the DC machine running, select the Windows 10 machine in VirtualBox.

#### Step 66:
- Click "Settings, then "Network", then switch the Adapter 1 to "Internal Network".

#### Step 67:
- Click "Start".

*(Skip through the install process until you fully login)*

#### Step 68:
- Hit the Start button and type "cmd" to open the Command Prompt.

#### Step 69:
- Type "ipconfig" to verify you have a correct IPv4 Address, Subnet Mask, and Default Gateway.

*(You can even ping a website like Google to test connectivity)*

![Step 69](https://github.com/user-attachments/assets/e7a722b0-a6af-4b1f-9fe1-c450974cf612)

#### Step 70:
- Go back your DC machines server dashboard, click "Tools", then click "DHCP".

#### Step 71:
- Click IPv4, click "Scope", then click "Address Leases" and view the client account you created.

![Step 71](https://github.com/user-attachments/assets/e7829f0d-fde7-47da-9aad-bb125dd4b407)

#
# CONGRATS!!! 
You have now successfully built your very own Active Directory!

![sparklepandalana-penguin](https://github.com/user-attachments/assets/b793aed5-3278-43d1-99a0-2aabc422db4e)

