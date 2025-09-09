<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />


# 🛠️ osTicket on Azure VM (Windows 10): Prerequisites and Installation

![Azure](https://img.shields.io/badge/Azure-Cloud-blue?logo=microsoft-azure)
![osTicket](https://img.shields.io/badge/osTicket-Support-orange)
![Windows](https://img.shields.io/badge/Windows-10-blue?logo=windows)

---

## 📌 Project Overview
This project documents the step-by-step installation of **osTicket v1.15.8** on an **Azure Virtual Machine running Windows 10**. It covers VM setup, IIS + PHP + MySQL configuration, osTicket deployment, and final security cleanup.

---

## 📑 Table of Contents
1. [Provision Azure Virtual Machine](#1-provision-azure-virtual-machine)
2. [Prepare Installation Files](#2-prepare-installation-files)
3. [Configure IIS and PHP](#3-configure-iis-and-php)
4. [Install and Configure MySQL](#4-install-and-configure-mysql)
5. [Configure IIS with PHP](#5-configure-iis-with-php)
6. [Deploy osTicket](#6-deploy-osticket)
7. [Enable PHP Extensions](#7-enable-php-extensions)
8. [Configure osTicket Files](#8-configure-osticket-files)
9. [Set Up osTicket Database](#9-set-up-osticket-database)
10. [Complete Web Installation](#10-complete-web-installation)
11. [Post-Installation Cleanup](#11-post-installation-cleanup)
12. [Architecture Diagram](#-architecture-diagram-optional)
13. [Next Steps](#-next-steps)

---

## 🚀 Installation Steps

### 1. Create an Azure Virtual Machine **I'll be using these VM Specifications for this project:**
- **Resource Group:** [Create new, any name you like that works]
- **Virtual Machine Name:** [Any name you like that works]
- **Image(OS):** Windows 10 Pro, version 22H2 
- **Size(vCPUs):** Standard_D2s_v3 - 2 vcpus, 8 GiB memory
- **Administrator Account:** Create new, *These credetials will be used to Log into the VM via           Remote Desktop for (WindowsOs)or Download Windows App for (MacOs)
<img width="1470" height="956" alt="vm setup pic 1" src="https://github.com/user-attachments/assets/62843094-f08a-4c96-8845-eecce420d6cc" />
---

### 2. Prepare Installation Files
- Inside the VM, download **osTicket-Installation-Files.zip**.
- Unzip to Desktop → Folder should be named **osTicket-Installation-Files**.
- All dependencies and installers will come from this folder.

---

### 3. Configure IIS and PHP
1. **Install IIS with CGI support:**
   - World Wide Web Services → Application Development Features → enable **CGI**.
2. From the installation folder, install:
   - **PHP Manager for IIS** (`PHPManagerForIIS_V1.5.0.msi`)
   - **Rewrite Module** (`rewrite_amd64_en-US.msi`)
3. Create a directory: `C:\PHP`
4. Extract **PHP 7.3.8** (`php-7.3.8-nts-Win32-VC15-x86.zip`) into `C:\PHP`
5. Install **VC_redist.x86.exe**

---

### 4. Install and Configure MySQL
1. From the installation folder, install **MySQL 5.5.62** (`mysql-5.5.62-win32.msi`).
2. Choose **Typical Setup** → Run Configuration Wizard → **Standard Configuration**.

---

### 5. Configure IIS with PHP
1. Open IIS **as Administrator**.
2. Register PHP with PHP Manager → point to: `C:\PHP\php-cgi.exe`
3. Restart IIS (Stop + Start the server).

---

### 6. Deploy osTicket
1. From the installation folder, unzip **osTicket v1.15.8**.
2. Copy the **upload** folder into `C:\inetpub\wwwroot`.
3. Rename `upload` → `osTicket`.
4. Restart IIS.
5. In IIS Manager → Sites → Default → osTicket → click **Browse *:80**.

---

### 7. Enable PHP Extensions
- In IIS → Sites → Default → osTicket → PHP Manager → Enable/Disable Extensions.
- Enable:
  - `php_imap.dll`
  - `php_intl.dll`
  - `php_opcache.dll`
- Refresh osTicket in the browser to confirm changes.

---

### 8. Configure osTicket Files
1. Rename configuration file:
   - From: `C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php`
   - To: `C:\inetpub\wwwroot\osTicket\include\ost-config.php`
2. Assign permissions:
   - Disable inheritance → Remove All
   - Add new permission: **Everyone → Full Control**

---

### 9. Set Up osTicket Database
1. Install **HeidiSQL** from installation folder.
2. Open HeidiSQL → create a new session 
3. Connect and create a new database: **osTicket**.

---

### 10. Complete Web Installation
1. In the osTicket browser setup:
   - Helpdesk Name: *Your Choice*
   - Default Email: (receives customer tickets)
   - MySQL Database: **osTicket**
   - Username: **root**
   - Password: **root**
2. Click **Install Now!**
3. Access URLs:
   - Admin/Staff Login: [http://localhost/osTicket/scp/login.php](http://localhost/osTicket/scp/login.php)
   - End User Portal: [http://localhost/osTicket/](http://localhost/osTicket/)

---

### 11. Post-Installation Cleanup
- Delete setup directory: `C:\inetpub\wwwroot\osTicket\setup`
- Set config file to read-only:
  - `C:\inetpub\wwwroot\osTicket\include\ost-config.php`

✅ osTicket is now fully installed and secured on your Azure VM!

---

## 📊 Architecture Diagram (Optional)
```mermaid
graph TD;
    User -->|Browser| AzureVM
    AzureVM -->|IIS + PHP| osTicket
    osTicket -->|MySQL| Database
```

---

## 📖 Next Steps
- Add SSL/TLS for secure access.
- Configure email piping/SMTP for ticket creation.
- Regularly back up MySQL and VM snapshots.

---

📌 **Author:** Your Name  
📌 **License:** MIT
