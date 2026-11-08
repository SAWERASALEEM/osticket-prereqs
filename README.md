<img width="700" height="200" alt="image" src="https://github.com/user-attachments/assets/4840ea94-c88e-4100-a29a-70e88acffe52" />


# OS Ticket Prerequisites & Installation

In this project we will be setting up the prerequisites and installing an open source ticketing system called "osTicket".


<h2>What is osTicket?</h2>
osTicket is an open-source helpdesk ticket management system. It is used by companies to manage customer problems and IT-related problems in one place.




<h2>Environments and Technologies Used</h2>

- Microsoft Azure
- Virtual Machines
- Remote Desktop
- Internet Information System (IIS)
- osTicket
- MySQL
- Heidi
- PHP

<h2>Operating Systems Used </h2> 

- Windows 11 Pro, version 25H2 - x64 Gen2

## Configuration Steps
1. Create an Azure Virtual Machine
2. Connect to the VM
3. Install IIS with CGI
4. Install dependencies
5. Register PHP with IIS manager
6. Load osTicket configuration file
7. Configure file permissions
8. Install & configure HeidiSQL
9. Finalize osTicket installation 

<h2>Deployment and Configuration Steps</h2> 





### Create a Resource Group
<img width="2876" height="1252" alt="image" src="https://github.com/user-attachments/assets/ddb466f6-076e-4301-ba8a-335486fe7171" />
<img width="2878" height="1348" alt="image" src="https://github.com/user-attachments/assets/999a010f-4391-43c5-8c6e-002218cb62f4" />
<img width="2878" height="1352" alt="image" src="https://github.com/user-attachments/assets/75f41f1b-649b-48e9-8d50-4b419c9a2db0" />


- Logged in to the Azure Portal and go the Resource Group.
- Once you are on the Resource Group click "CREATE"
- Give the resource group name as "osTicket"
- Select the appropriate region. I chose "EAST US 2"
- Click CREATE 





### Create an Azure Virtual Machine

We will create a Virtual Machine in "Windows 11 Pro, version 25H2 - x64 Gen2"

<img width="2878" height="1330" alt="image" src="https://github.com/user-attachments/assets/22e8c879-2c83-4ada-b512-a2e918d4c1ae" />
- Now we create a Virtual Machine
- Click Create

<img width="2098" height="1354" alt="image" src="https://github.com/user-attachments/assets/316da3a0-299e-4789-9471-65ae19005f60" />
- Select the Resource Group   ->Give a Virtual Machine a NAME   ->Select the Region
  
<img width="2132" height="1352" alt="image" src="https://github.com/user-attachments/assets/d1dedf1e-cbcc-46df-a3e7-b9679a56e063" />
- Select the Image   -> Select the Size
  
<img width="2158" height="1358" alt="image" src="https://github.com/user-attachments/assets/d5ec93c0-8cc2-4c2d-8ecd-9d8d48312011" />
Create a USERNAME and PASSWORD

<img width="2164" height="1358" alt="image" src="https://github.com/user-attachments/assets/8d6fd289-2cfb-4fa9-869f-6cdb3f6e6a6f" />
Be sure to check "*I confirm I have an eligible Windows 10/11 license with multi-tenant hosting rights.*"  

<img width="2168" height="1364" alt="image" src="https://github.com/user-attachments/assets/ad84aa21-581f-4133-b0bd-f0c9316c2a88" />
Go to the Review+create and then click CREATE

<img width="2880" height="1240" alt="image" src="https://github.com/user-attachments/assets/2e970ee9-82ee-48e6-9aca-7015532a445e" />
VIRTUAL MACHINE deployment is in progress


<img width="2880" height="1318" alt="image" src="https://github.com/user-attachments/assets/cffeee70-c724-4fc5-83c9-7f8163ac2ab6" />
Virtual Machine has been Created




| Selection             | Configuration                           |
| --------------------- | --------------------------------------- |
| Resource group:       | OSTicket                                |
| Virtual machine name: | OSTicket-vm                             |
| Region                | I chose East US 2                       |
| Image:                | Windows 11 Pro, version 25H2 - x64 Gen2 |
| Size:                 | Standard_D2ads_v6 - 2 vcpus,8 GiB memory|
| Username              | Labuser                                 |
| Password              | Password1234                            |



### Connect to  the VM:

<img width="2878" height="1262" alt="image" src="https://github.com/user-attachments/assets/96cde874-0bb1-4092-a92b-aed7dd9517b3" />
 <img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/ea1d5b9b-8efb-468f-8f4f-9d951c2e0a05" />
<img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/636da8c5-cbe0-4239-ba61-0a35bcc9a191" />
<img width="2866" height="1800" alt="image" src="https://github.com/user-attachments/assets/04ca25ce-7034-4418-b5be-cea4251de3fe" />

- First you need to copy the Public IP Address
- Open the Remote Desktop App and select the add PC option
- After that you need to put the IP Address and select the pc name as "osTicket' and click add
- Type username and Password and click continue

- USERNAME: `labadmin`
- PASSWORD: `Password1234`

- Now we have successfully created a remote desktop


### Installing IIS with CGI

Next we will be installing and enabling IIS (Internet Information Services) with CGI
To do this navigate to the Control Panel

<img width="2872" height="1800" alt="image" src="https://github.com/user-attachments/assets/48608cad-36cb-414f-9ce1-3b264dc35b12" />
<img width="2010" height="1116" alt="image" src="https://github.com/user-attachments/assets/f0bd898d-2771-4828-9d25-fa526acc5d28" />



 Click on Programs> Turn Windows Features On or Off

![Pasted image 20250313054637](https://github.com/user-attachments/assets/bef5dc7f-2b55-44a1-aa56-a34f9981a120)

 Tick Internet Information Services (IIS)
 
 Navigate to World Wide Web Services> Application Development Features and tick CGI box

<img width="2880" height="1800" alt="image" src="https://github.com/user-attachments/assets/9543cd65-cc17-4536-af9c-7ec594474d25" />

### Verify IIS has been installed

Navigate to the web browser and type http://127.0.0.1/ you should see this screen:

*This address is the loopback address we have created a website hosted on the internal loopback address*

![Pasted image 20250313055435](https://github.com/user-attachments/assets/ba2a6cd2-f5f0-438a-8e61-1e3ded145c6a)

### Installing dependencies

#### Install PHP manager for IIS

All the necessary files can be found [here](https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0) open this link within the VM and download the files and unzip them to the desktop

Install PHPManagerForllS_V1.5.O

*Click through all prompts as necessary*

![Pasted image 20250313060044](https://github.com/user-attachments/assets/1f601558-2794-4e95-8e5a-2333ea9c5d51)


![Pasted image 20250313060632](https://github.com/user-attachments/assets/38be9458-e5e0-4593-a5a2-895086ace18f)


#### Install "rewrite_amd64_en-US"

Next install "rewrite_amd64_en-US"

*Click through all prompts as necessary*

![Pasted image 20250313060742](https://github.com/user-attachments/assets/7e9761ef-f153-47b6-b4c9-49dc3da6401e)


![Pasted image 20250313060853](https://github.com/user-attachments/assets/4c373444-0c95-415c-af3a-4c6db683518f)


#### Create a directory on C drive named PHP

Navigate to `C:` > Create a folder named `PHP`

![Pasted image 20250313061042](https://github.com/user-attachments/assets/2342c8c5-465d-4036-a74d-cc56d2126003)


unzip the contents  of "php-7.3.8-nts-Win32-VC15-x86" into the directory we just created

![Pasted image 20250313061247](https://github.com/user-attachments/assets/b103520b-4200-4010-a955-77257af04b97)


PHP folder will look like this after: 
![Pasted image 20250313061418](https://github.com/user-attachments/assets/265b14b8-6c2f-471b-977a-3c78091a41c5)


#### Next install "VC_redist.x86"

Next install "VC_redist.x86"

Click through all prompts as necessary

![Pasted image 20250313061526](https://github.com/user-attachments/assets/b7a9318e-853b-4f88-97bb-8e266adfb30d)


![Pasted image 20250313061607](https://github.com/user-attachments/assets/250742ef-1d53-48fd-82a9-ed6d32ff4636)


#### Install "mysql-5.5.62-win32"

![Pasted image 20250313061704](https://github.com/user-attachments/assets/49e29025-6af7-474b-bb75-a029ba8fb0b9)


When you get to this screen choose "Typical" and install

![Pasted image 20250313061800](https://github.com/user-attachments/assets/5912623a-4f81-468f-bf29-88af1f50b2b7)


Tick "launch the MySQL Instance Configuration Wizard" and click finish

![Pasted image 20250313061846](https://github.com/user-attachments/assets/27794559-d6b7-440b-a7f2-f96c35408496)


Click "Standard Configuration"

![Pasted image 20250313062105](https://github.com/user-attachments/assets/38c2eb11-c504-47aa-ba0e-9a1ca7a3586f)


Configure root password as: `osTicketPassword123!`  

![Pasted image 20250313062301](https://github.com/user-attachments/assets/e2dbc651-fa99-41a6-b5bd-17f6a5bbc1ab)

#### Register PHP with IIS manager

Open IIS manager run as admin

![7](https://github.com/user-attachments/assets/dbbb7338-4e8d-4561-b012-41b13c7c77f9)


Click on "PHP manager"  

![Pasted image 20250313063120](https://github.com/user-attachments/assets/a8e27bbd-e1a5-4616-9f09-6a237d814bb7)


Click on "Register new PHP version"

![Pasted image 20250313063207](https://github.com/user-attachments/assets/65830c14-0678-414a-b736-c148f31a598f)


Next configure the path `C:\PHP\php-cgi.exe` and click ok 

![Pasted image 20250313063329](https://github.com/user-attachments/assets/98a41d33-57a8-4db2-bba8-912a05b5802e)



Restart IIS for the change to take effect

![Pasted image 20250313063523](https://github.com/user-attachments/assets/6747c5af-857a-4969-bb14-226e9e172e7a)


### Install OSTicket v1.15.8

Extract the zipped files 

![Pasted image 20250313063721](https://github.com/user-attachments/assets/fc83dd23-2df6-481d-b21f-855701fc5064)


It should look like this:

![Pasted image 20250313064213](https://github.com/user-attachments/assets/a6b06ecb-e13a-41a0-9758-a50b33c38086)



Copy the "upload folder" to `c:\inetpub\wwwroot` then rename "upload" to `osTicket`

![Pasted image 20250313064325](https://github.com/user-attachments/assets/0087caa8-69bc-46cc-a77b-4386cf9ab208)

Restart IIS for the change to take effect

![Pasted image 20250313063523](https://github.com/user-attachments/assets/b9d062d6-05c8-49ab-ac62-e0e83c2d3b8e)


On IIS go to osticket and then click "Browse"

![Pasted image 20250313064808](https://github.com/user-attachments/assets/6f14c1fd-4989-45c2-9deb-89ce80774bef)


You should be met with the osTicket installer: 

As you can see by the red Xs we still have a bit more to configure 

![Pasted image 20250313064852](https://github.com/user-attachments/assets/8d2ee7ab-ee48-4922-80ef-2ea11d59ce36)

#### Enable PHP Extensions
   
![Pasted image 20250313165524](https://github.com/user-attachments/assets/6238347a-fae4-4f8c-885e-57602f6a9f99)

![Pasted image 20250313165618](https://github.com/user-attachments/assets/7eb1e3e3-a9d6-4db9-9fda-59bdddfd78a7)

![Pasted image 20250313165936](https://github.com/user-attachments/assets/29fdc3b8-4cff-4062-920e-991b3a3d9216)


Once your done it should look like this:

![Pasted image 20250313170211](https://github.com/user-attachments/assets/5e26433f-859a-48ae-a20b-67ae42ef67ff)

- Go back to IIS > Sites > Default Web Site > osTicket
- Double-click PHP Manager
- Click “Enable or Disable an Extension” at the bottom of the screen under PHP Extensions
- Right-click and enable the following
- php_imap.dll (Might be already enabled)
- php_intl.dll
-php_opcache.dll

Now we can go back to our web browser and refresh to see if the changes updated

The two red Xs remaining are not necessary for osTicket to function properly for our purposes we wont be enabling them

It should look like this:

![Pasted image 20250313170707](https://github.com/user-attachments/assets/58e5268a-638c-4012-b06d-9f33f8669f31)



#### Rename `ost-sampleconfig.php`
- Open Windows Explorer and select C: > inetpub > wwwroot > osTicket > include
- Rename`ost-sampleconfig.php`to `ost-config.php`

![Pasted image 20250313171115](https://github.com/user-attachments/assets/3ce22f25-5663-45e0-893b-9601816d6bf3)

Renamed:

![Pasted image 20250313171148](https://github.com/user-attachments/assets/31d3a47a-a4f6-4be4-9c33-85c9828ca9ec)



#### Assign permissions to `ost-config.php`

- Right-click ost-config.php
- Open Properties > Security > Advanced > Permissions
- Select Disable Inheritance > Remove all inherited permissions from this object

![8](https://github.com/user-attachments/assets/4f2261ab-a420-4bd3-9289-2622e7644db3)

![Pasted image 20250313172029](https://github.com/user-attachments/assets/1608fde9-aa19-4c5c-b748-25c16209b8e6)

![Pasted image 20250313172209](https://github.com/user-attachments/assets/076c1728-7972-4578-be90-0db8a2154f1b)


- Afterwards, select Add > select Principal > type in "everyone" > select Check Names > select OK
- Allow everyone full control (check all boxes) > Select apply > OK

![Pasted image 20250313172441](https://github.com/user-attachments/assets/6381496e-addc-4539-af7d-9abd5ec32e2d)



![Pasted image 20250313172553](https://github.com/user-attachments/assets/6780b167-ddab-4461-9b1a-f89ed6b58045)


![Pasted image 20250313172819](https://github.com/user-attachments/assets/48ee9478-e4d7-445b-ab40-8d2abce5db58)


![Pasted image 20250313172917](https://github.com/user-attachments/assets/54373c1b-cc6e-4d3c-94b0-e9b0d73291b7)


### Next install & Configure HeidiSQL

![Pasted image 20250313173556](https://github.com/user-attachments/assets/f02d9fcd-e78b-40e5-a8f8-bf70bc5b44aa)


After you finish installing launch HeidiSQL


![Pasted image 20250313173937](https://github.com/user-attachments/assets/e6cc680e-e690-40ce-b646-d4b3190967d8)


![Pasted image 20250313174539](https://github.com/user-attachments/assets/1053301a-252d-459e-8622-c72eca363f0f)


- Open HeidiSQL > Select "New" at the bottom-left corner of the screen
- User: root
- Password: Password1
- Select Open
- On the left side, right-click Unnamed > select Create New > Database
- Name it “osTicket” and select OK

Note: You must name it exactly `osTicket` with the T capitalized or the configuration will not work 

![Pasted image 20250313174332](https://github.com/user-attachments/assets/1127e6f9-2b3e-4fc9-aae3-b76c2c7b931e)

### Finalize osTicket installation

Now back on the web browser we will click "continue" to continue the install 
<p align="center">
<img src="https://i.imgur.com/1GfpPLs.png" height="80%" width="80%" alt="Azure Free Account"/>

Configure the following sections:



| Selection      | Configuration             |
| -------------- | ------------------------- |
| Helpdesk Name  | Helpdesk                  |
| Default Email  | example-email@gmail.com   |
| First Name     | your first name           |
| Last Name      | your last name            |
| Email Address  | example-email-2@gmail.com |
| Username       | user_admin                |
| Password       | Password1                 |
| MySQL Database | osTicket                  |
| MySQL Username | root                      |
| MySQL Password | Password1                 |




![Pasted image 20250313175410](https://github.com/user-attachments/assets/5fb69155-680a-4eeb-bd74-0b2fdc142108)



Now if we navigate to: http://localhost/osTicket/  

We will be greeted by the customer facing portal 

![Pasted image 20250317053047](https://github.com/user-attachments/assets/405b2548-1748-4df4-8745-c162cba8fd95)



If we navigate to http://localhost/osTicket/scp/login.php  
We will be greeted by the employee/admin login page  
We can use the following credentials to login to the admin portal   

| Selection | Configuration        |
| --------- | -------------------- |
| Username  | user_admin           |
| Password  | Password1            |

![Pasted image 20250317053218](https://github.com/user-attachments/assets/540eda21-9c23-4430-abb7-25ac529a9a95)

Thats it for this lab we have successfully installed osTicket!



