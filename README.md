<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Microsoft Remote Desktop (RDP)
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>List of Prerequisites</h2>

- Azure Virtual Machine
- osTicket Installation Files
- Heidi SQL

<h2>Installation Steps<h2>

 ### Create an Azure Virtual Machine 
 - Within Azure, go search up Virtual Machines → Create → Virtual Machine

![project VM create pic](https://github.com/user-attachments/assets/a7760116-01d0-4518-93e0-20f2510595e0)

---

- Now, in order for Azure to create/validate the virtual machine, you must enter desired credentials and ONLY have to modify the settings mentioned below (all other settings can be left alone/default)

- **Resource Group:** [Create new, any name you like that works]
- **Virtual Machine Name:** [Any name you like that works]
- **Image(OS):** Windows 10 Pro, version 22H2 
- **Size(vCPUs):** Standard_D2s_v3 - 2 vcpus, 8 GiB memory
- **Administrator Account:** Create new, *These credetials will be used to Log into the VM via Remote       Desktop App (MacOs)
    
<img width="1470" height="956" alt="vm setup pic 1" src="https://github.com/user-attachments/assets/62843094-f08a-4c96-8845-eecce420d6cc" />

![vm create pic 2](https://github.com/user-attachments/assets/65dad87f-c0c5-4557-9e28-6e975587023e)

- Once this is complete, you can click on "Review+Create"


---

- Azure will then run a Validation process. If previous steps are completed correctly, you will be brought to this screen stating "Validation passed"

![project pic VM validation passed](https://github.com/user-attachments/assets/11778173-f1b9-4bc9-ac09-e24104a100e8)


 - You may now click "Create" and deployment process of your virtual machine will now take place

![vm deployment process](https://github.com/user-attachments/assets/3cdbeb01-9d5e-4fb6-b17f-be9490ffddba)


 - Once process finishes, screen will tell you "Your deployment is complete"


![vm deployment complete](https://github.com/user-attachments/assets/84966319-b46d-4b53-90b8-72e79de0c20a)



---


### Loging into Virtual Machine and Preparing Installation Files

Once VM deployment is complete, we are going to open the Remote Desktop app and add a PC 

![add a pc for vm](https://github.com/user-attachments/assets/e59fec26-0964-431b-8883-d3d2dad8c288)

It is going to require a host name/PC name, which you will use the Public IP Address of the virtual machine you just created within Azure

![vm ip address for RDC app login](https://github.com/user-attachments/assets/db21c0d5-d5b4-4f90-a472-47f830fc74b7)


- You can also give the virtual machine a name to properly identify it (for this project we'll use "osTicket"). Once thats entered, it should look something like this 

![vm ip for rdc login 2](https://github.com/user-attachments/assets/4bd7a881-676f-41bb-9cee-0adb8f92b8ef)


- Select "ADD" and you now have a created virtual machine that is ready to operate

![vm created ready to login](https://github.com/user-attachments/assets/62cfae2b-c06e-4110-864a-4a4cc8bb07d5)


Next, we are going to select the virtual machine within the Remote Desktop app and login using the same Administrator Account credentials that you used to create the Virtual machine within Azure (in the previous beginning steps)

![rdc app login](https://github.com/user-attachments/assets/bb9835f0-9501-465d-9e91-09ea394a42d1)


- The actual virtual machine will then open and begin loading

![rdc actually logging in](https://github.com/user-attachments/assets/c60a7ffc-cf49-4fba-a50d-0756a88f1c9e)



![rdc loaded up](https://github.com/user-attachments/assets/893d6e68-7b30-471a-958b-bba9d00e2a1d)

 
 - After loading, you have successfully logged into the virtual machine you created!




**Note: Everything from here on out will be done the the Virtual Machine only.**

---

- Copy this link (osTicket Installation Files): (https://drive.usercontent.google.com/download?id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD&export=download&authuser=0)    (all dependencies and installers will come from this folder)
- Within the virtual machine open up Microsoft Edge web browser and paste the (osTicket Installation Files) link above in the browser's search bar and enter

 
![osTicket files link copy and paste](https://github.com/user-attachments/assets/61421611-39ee-4053-bb71-94855749bee7)



![osTicket files link enterd](https://github.com/user-attachments/assets/9eda99bd-effc-4a93-b883-f555c75a5506)

- It'll bring you to this page, select "Download anyway"  




- Once download completes open **osTicket-Installation-Files.zip**, it will take you to the downloads folder, from there click and drag it to Desktop → then (right click) Extraxt All → (should be named **osTicket-Installation-Files**) select "Extract"


![osTicket file on desktop](https://github.com/user-attachments/assets/bcb8c7f5-5c6a-4928-8b9e-608c96ffb80f)

![extract osTicket files](https://github.com/user-attachments/assets/78a3f9a9-5503-4316-bb70-8c938a86583f)

- The File folder "osTicket-Installation-Files" should pop up


![osTicket folder](https://github.com/user-attachments/assets/0f038d27-32b6-4033-a28f-27ba7c85d3c3)

![osTicket folder opened](https://github.com/user-attachments/assets/249d4bf0-fbe8-4d07-ac5e-d0ac31c2317a)

 - As you you can see it is containing all of the file dependencies and installers inside of the folder

 - **Optional:** Feel free to delete the original **osTicket-Installation-Files.zip** (icon with actual zipper on it), since we unziped the file and now have everything we need in the new **osTick-Installation-Files** folder
 

 ---
 
 
### Install IIS with CGI support

 - Go to Start Menu → Contorl Panel → Uninstall a program → Select Turn windows features on or off (on the left side) → Enable Internet Information Services **(IIS)** → World Wide Web Services → Application Development Features → Enable **CGI** → OK

   
![CGI install](https://github.com/user-attachments/assets/a6fc5f7c-0b03-4498-aa4e-e229611a0f48)


 - Allow a moment for install to finish and it will let you know it is complete

  
![CGI install process](https://github.com/user-attachments/assets/c4d3428d-9f95-4e10-a012-7ba685d1c13f)

![CGI completed](https://github.com/user-attachments/assets/71dbf847-4d70-4500-8814-b82f9a302beb)


---
 
 
 
 
 ### Installing PHP Manager & Rewrite Module
  
 - From **osTicket-Installation-Files** → Install **PHPManagerForIIS_V1.5.0** & **rewrite_amd64_en-US** (* Double-click individually and go through each installation seperately)


<img width="1470" height="956" alt="project pic7" src="https://github.com/user-attachments/assets/9f45bdc8-b64a-4154-bcaa-627e8877dfa2" />



- PHP Manager Install
![PHP manager install](https://github.com/user-attachments/assets/4e55c2c0-5290-43aa-b1aa-160fe620674b)


- Rewrite Module Install
![rewrite module install](https://github.com/user-attachments/assets/899d7803-e9fc-4d2d-b11d-afe4fa5b8f73)

 ---
 
 ### Create a directory on C:\PHP & Install Visual C++ Redistributable

- Go to File Exploer → This PC → Windows(C:) → create new folder(Titled "PHP")
  

![Create directory PHP folder](https://github.com/user-attachments/assets/a3a2d42c-9e41-4f93-b6be-2ad4d8d71307)



- Go back to **osTicket-Installation-Files** → (right-click) **php-7.3.8-nts-Win32-VC15-x86.zip** → Extract All → Browse → Windows (C:) → PHP → Extract
   

<img width="1470" height="956" alt="project pic10" src="https://github.com/user-attachments/assets/e343be60-6a94-47d9-9fc5-533f671cdba6" />


- As you can see all Extracted files are now in the PHP folder you just created

![PHP zip files extracted to PHP folder](https://github.com/user-attachments/assets/f3ff5709-6efc-424d-b8f5-d324ba347c37)
  
   
   
- Next, go back in **osTicket-Installation-Files** → (Double-click) **VC_redist.x86.exe** and go through install

![VC install](https://github.com/user-attachments/assets/60294686-1b1b-49cc-82bf-5045dec17017)

![VC install complete](https://github.com/user-attachments/assets/5b41f60c-ea45-4b3a-90ce-59210ee1e75a)

---


### Install and Configure MySQL

- Go to **osTicket-Installation-Files** → (double-click) **mysql-5.5.62-win32.msi** → (throughout install) select Typical Setup → Run Configuration Wizard → Standard Configuration → Modify Security Settings, New root password: root & Confirm: root → Execute → Finish


![MYSQL install](https://github.com/user-attachments/assets/95aa71da-53ee-4ccb-a870-933317ccd0d3)

![MYSQL install 2](https://github.com/user-attachments/assets/acb0d0a5-7e9b-4101-a919-a9494cf146ea)



**username: root**
**&** **password: root**
(simplie credentials for the sake of this project)   
![MYSQL install 3](https://github.com/user-attachments/assets/05f67aaa-461a-4878-b257-5a33d97b9124)


![MYSQL install finish](https://github.com/user-attachments/assets/085e595c-27a5-43a1-8a74-cb2b253e99c1)


---


### Configure IIS with PHP (Register PHP with PHP Manager)

- Start (Menu) → Type IIS(Internet Information Services) → Run as Administrator → PHP Manager → Register new PHP version → Browse → Windows (C:) → PHP → php-cgi → Open → Ok
  
![configure IIs](https://github.com/user-attachments/assets/a2f2d553-b7f0-414a-ac81-3efd9771e392)

![configure IIS 2](https://github.com/user-attachments/assets/df68d715-a037-43f6-b12c-1990307beceb)


- Now restart IIS within IIS Manager by right-clicking server **osTicket-vm** → Stop (wait a moment) → Start

![configure IIS 3](https://github.com/user-attachments/assets/32451ff3-1f56-414b-82fd-cec27613b9e4)




### Deploy osTicket

- Go back **osTicket-Installation-Files** → (right-click) osTicket v1.15.8 → Extrat All, with in the same folder which creates a separate folder osTicket v1.15.8 (at the top)


<img width="1470" height="956" alt="project pic13" src="https://github.com/user-attachments/assets/89932447-c642-4e6a-8711-46c8339b5092" />


Click into the newly created file folder **osTicket v1.15.8**(not the zip folder) → Copy the upload folder → Windows(C:) → inetpub → wwwroot → paste


<img width="1470" height="956" alt="project pic14" src="https://github.com/user-attachments/assets/80f70798-bd9f-4c00-87b7-398262834d6c" />


Rename "upload" to "osTicket"(exactly how its spelled) → restart IIS agagin by right-clicking server(osTicket-vm-name) → Stop (wait a moment) → Start


In IIS Manager → server(osTicket-vm-name) → Sites → Default Web Site → osTicket → Browse *:80(http)


That should bring up osTicket


<img width="1470" height="956" alt="project pic15" src="https://github.com/user-attachments/assets/094d7397-8c56-4e16-a7a2-a3e21b6d678b" />


---


### 7. Enable PHP Extensions that are Disabled (in previous picture)

- In IIS → Sites → Default → osTicket → PHP Manager (double-click) → Enable or Disable an Extension
- Find and Enable:
  - php_imap.dll 
  - php_intl.dll
  - php_opcache.dll
- Refresh osTicket in the browser to confirm changes.


<img width="1470" height="956" alt="project pic16" src="https://github.com/user-attachments/assets/8b77a597-935d-44d0-99fd-35b85b1e928f" />


Notice a few more PHP Extensions are now checked green
 

### 8. Configure osTicket Files

-  Rename configuration file and assign permissions
 
 -  File Exploer → This PC  → windows(C:) → inetpub → wwwroot → osTicket → include → find **ost-sampleconfig.php** (right-click) → Rename → **ost-config.php** 

-  **ost-config.php**(right-click) → properties → Security → Advanced → Diable inheritance → Remove all inherited permissions from this object → Add → Select a principal → 'type' Everyone (for the sake of the project) → Check Names → OK → check Full control → Apply → OK


<img width="1470" height="956" alt="project pic17" src="https://github.com/user-attachments/assets/b70d4fa7-3f25-4521-b741-ec16f54ff11b" />


---


### 9. Set Up osTicket Database

Go to **osTicket-Installation-Files** on the Desktop → HeidiSQL_12.3.0.6589_Setup → Install → skip → New →
Username: **root** & Password: **root** → Open → Unnamed(right-click) → Create New → Database → 
Name: osTicket → OK


<img width="1470" height="956" alt="project pic18" src="https://github.com/user-attachments/assets/469d8e6c-164e-4474-be5c-baca1e9f4e0a" />





---


### 10. Complete Web Installation

Go back to osTicket website in web browser → Press Continue → Fill out osTicket Basic Installation - System Settings and Admin User areas with your own information 

For Database Settings put these specifics(for the sake of the lab) →

MySQL Database: **osTicket**
MySQL Username: **root**
MySQL Password: **root**

 Click **Install Now!**


<img width="1470" height="956" alt="project pic19" src="https://github.com/user-attachments/assets/46677e79-c185-41b2-ad95-c3893d3bcd93" />


 ***osTicket is Officially UP and Ready to Operate***


 ---

 
 Access URLs:
   
   
   - Admin/Staff Login: [http://localhost/osTicket/scp/login.php](http://localhost/osTicket/scp/login.php)
   
   
   <img width="1470" height="956" alt="project pic20" src="https://github.com/user-attachments/assets/06fa8890-5dce-4212-a699-29b1f5145d58" />

   
   
   
  
   
   - End User Portal: [http://localhost/osTicket/](http://localhost/osTicket/)

  
   <img width="1470" height="956" alt="project pic21" src="https://github.com/user-attachments/assets/1a12a927-7771-4765-8d6a-2f2a0c51f271" />


---


✅ **osTicket is now fully installed and secured on your Azure VM!**

---

##  Architecture Diagram 
```mermaid
graph TD;
    User -->|Browser| AzureVM
    AzureVM -->|IIS + PHP| osTicket
    osTicket -->|MySQL| Database
```

---

 **Author:** Ed Latimer
