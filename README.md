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
---

##  Installation Steps

### Create an Azure Virtual Machine 

- **Resource Group:** [Create new, any name you like that works]
- **Virtual Machine Name:** [Any name you like that works]
- **Image(OS):** Windows 10 Pro, version 22H2 
- **Size(vCPUs):** Standard_D2s_v3 - 2 vcpus, 8 GiB memory
- **Administrator Account:** Create new, *These credetials will be used to Log into the VM via Remote Desktop for (WindowsOs)or Download Windows App for (MacOs)

<img width="1470" height="956" alt="vm setup pic 1" src="https://github.com/user-attachments/assets/62843094-f08a-4c96-8845-eecce420d6cc" />

---


### Prepare Installation Files

- Once VM deployment is complete, add a PC in the Windows App(Remote Desktop) using the IP address      of the VM in Azure, then log into the VM using the adminsistrator account credentials

 <img width="1470" height="956" alt="vm pic 3" src="https://github.com/user-attachments/assets/5781215f-5740-4cbd-b97f-2263d8d02b56" />

- I have provided a link here:(https://docs.google.com/document/d/1DyjX8LeVU98LjhXO2t2K2F0aHywI2N9GD57T3taO5qo/edit?tab=t.0) This link will provide with everything you need to get osTicket up and operating.
- Download **osTicket-Installation-Files.zip**, Unzip to Desktop → Folder should be named **osTicket-Installation-Files** (all dependencies and installers will come from this folder)


<img width="1470" height="956" alt="project pic" src="https://github.com/user-attachments/assets/60d26a09-49ee-44de-ada7-76d73c71c082" />


<img width="1470" height="956" alt="project pic5" src="https://github.com/user-attachments/assets/e11d2669-3a3f-48ab-8cc1-5d7606436232" />


---


### Install IIS with CGI support

   -  Go to Contorl Panel → Uninstall a program → Select Turn windows features on or off (on the left       side) → Enable Internet Information Services **(IIS)** → World Wide Web Services → Application Development Features → Enable **CGI**.


<img width="1470" height="956" alt="project pic6" src="https://github.com/user-attachments/assets/f8becf06-598f-4cc0-9a63-209146696e31" />

  
   -  From **osTicket-Installation-Files** → Install **PHPManagerForIIS_V1.5.0** & **rewrite_amd64_en-US** (*Install individually by double-clicking each one seperately)


<img width="1470" height="956" alt="project pic7" src="https://github.com/user-attachments/assets/9f45bdc8-b64a-4154-bcaa-627e8877dfa2" />

  
   - **Create a directory:** Go to File Exploer → This PC → Windows(C:) → create new folder(Titled "PHP")
  
  
   -  Go back to **osTicket-Installation-Files** → (right-click) php-7.3.8-nts-Win32-VC15-x86.zip → Extract All → Browse → Windows (C:) → PHP → Extract
   


<img width="1470" height="956" alt="project pic10" src="https://github.com/user-attachments/assets/e343be60-6a94-47d9-9fc5-533f671cdba6" />

  
   - Also in **osTicket-Installation-Files** → install VC_redist.x86.exe (double-click)


---


### Install and Configure MySQL

   From **osTicket-Installation-Files** → install mysql-5.5.62-win32.msi (double-click) → 
   (throughout install) select Typical Setup → Run Configuration Wizard → Standard    
Configuration → Modify Security Settings, New root password & Confirm: root → Execute

username: root

password: root

(simplie credentials for the sake of this project)   

<img width="1470" height="956" alt="project pic11" src="https://github.com/user-attachments/assets/581cd80d-5041-40b8-9d61-d2435cd178dd" />


---


### 5. Configure IIS with PHP (Register PHP with PHP Manager)

-  Start (Menu) → type IIS(Internet Information Services) → Run as Administrator → PHP Manager → Register new PHP version → Browse → Windows (C:) → PHP → php-cgi → open


-  Restart IIS by right-clicking server(osTicket-vm-name) → Stop (wait a moment) → Start


<img width="1470" height="956" alt="project pic12" src="https://github.com/user-attachments/assets/9c5aee7d-63a5-44ad-b1b8-cdddba0283cc" />


### 6. Deploy osTicket

-  From **osTicket-Installation-Files** → (right-click) osTicket v1.15.8 → Extrat All, with in the same folder which creates a separate folder osTicket v1.15.8 (at the top)


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
