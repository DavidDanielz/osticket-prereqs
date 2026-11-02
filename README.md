<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1 align="center">osTicket – Prerequisites & Installation (Lab)</h1>

<p align="center">
  End-to-end technical deployment of the osTicket help desk system on Microsoft Azure
</p>

---

## 📌 Overview

This lab demonstrates the **full technical installation and configuration** of **osTicket**, an open-source help desk ticketing system, deployed on a **Microsoft Azure-hosted Windows virtual machine**.

The walkthrough documents each step performed during deployment, including virtual machine provisioning, IIS configuration, PHP installation, MySQL database setup, and osTicket installation.

All screenshots were captured **during execution** to demonstrate how the system was built from start to finish.

---

## 🖥️ Environment

- Microsoft Azure (Virtual Machines)
- Windows 11 Pro
- Internet Information Services (IIS) with CGI
- PHP 7.3.8
- MySQL Server 5.5
- Remote Desktop Protocol (RDP)
- HeidiSQL

---

## ⚙️ Installation & Configuration Steps

---

### **Step 1: Provision Azure Virtual Machine**
<img src="19. osTicket-VM created (Virtual machines).png" width="80%" alt="Azure VM Creation"/>

Create a Windows 11 virtual machine in Microsoft Azure to host the osTicket environment.

---

### **Step 2: Connect via Remote Desktop**
<img src="21.5 Proof of Connecting to VM .png" width="80%" alt="RDP Login"/>

Connect to the Azure virtual machine using Remote Desktop Protocol to begin configuration.

---

### **Step 3: Download osTicket Installation Files**
<img src="23. osTicket-installation-files (All).png" width="80%" alt="Download Files"/>

Download and extract the osTicket installation package and required components inside the virtual machine.

---

### **Step 4: Install IIS with CGI Enabled**
<div style="display: flex; gap: 10px;">
  <img src="29. Click IIS to World Wide Web Services .png" width="45%" alt="IIS Features"/>
  <img src="30. Click IIS to WWWS to Application Development Features to check off CGI.png" width="45%" alt="CGI Enabled"/>
</div>

Enable Internet Information Services (IIS) and select CGI under Application Development Features.

---

### **Step 5: Install IIS Dependencies**
<div style="display: flex; gap: 10px;">
  <img src="32. PHP Manager for IIS setup.png" width="45%" alt="PHP Manager"/>
  <img src="33. IIS URL Rewrite Module 2 Setup.png" width="45%" alt="URL Rewrite"/>
</div>

Install PHP Manager for IIS and the IIS URL Rewrite Module.

---

### **Step 6: Install PHP Runtime**
<img src="38. Extract_Select Destination_C to PHP.png" width="80%" alt="PHP Install"/>

Create the `C:\PHP` directory and extract PHP 7.3.8 to this location.

---

### **Step 7: Install Microsoft Visual C++ Redistributable**
<img src="40. Microsoft Visual C++ Install.png" width="80%" alt="VC++ Install"/>

Install the Microsoft Visual C++ Redistributable required by PHP and MySQL.

---

### **Step 8: Install MySQL Server**
<img src="41. Install MySQL Server 5.5.png" width="80%" alt="MySQL Install"/>

Install MySQL Server to serve as the backend database for osTicket.

---

### **Step 9: Register PHP in IIS**
<img src="44. Click PHP Manager in IIS.png" width="80%" alt="PHP Manager"/>
<img src="47. Register new PHP version.png" width="80%" alt="Register PHP"/>

Use PHP Manager in IIS to register `php-cgi.exe` and apply the configuration.

---

### **Step 10: Deploy osTicket Application Files**
<img src="52. Taking (upload) folder and adding it to the wwwroot folder.png" width="80%" alt="Initial Folder Structure"/>

Move the `upload` directory from the extracted osTicket files into `C:\inetpub\wwwroot`.

<img src="53. upload in wwwroot.png" width="80%" alt="Upload Folder"/>

Rename the `upload` directory to `osTicket`.

<img src="54. Change upload name to osTicket.png" width="80%" alt="Renamed Folder"/>

---

### **Step 11: Launch osTicket Web Installer**
<img src="58. osTicket installer Prerequisites with missing some extensions.png" width="80%" alt="Installer Prerequisites"/>

Access the osTicket installer through a web browser and review prerequisite warnings.

---

### **Step 12: Configure PHP Extensions**
<img src="63. Refresh osTicket installer page and extensions are added. .png" width="80%" alt="Extensions Enabled"/>

Enable required PHP extensions and refresh the installer until all prerequisites pass.

---

### **Step 13: Configure osTicket Configuration File**
<img src="69. Advanced Security settings for ost-config.php.png" width="80%" alt="Config Permissions"/>

Rename `ost-sampleconfig.php` to `ost-config.php` and assign temporary write permissions.

---

### **Step 13a: Installer Database Requirement**
<img src="76. osTicket system_admin user_database settings basic installation setup.png" width="80%" alt="Database Required"/>

The installer requires database credentials before installation can proceed.

---

### **Step 14: Create Database with HeidiSQL**
<img src="87. Refresh osTicket in HeidiSQL and see that it's not emoty anymore.png" width="80%" alt="HeidiSQL Database"/>

Create the osTicket database and database user using HeidiSQL.

---

### **Step 15: Complete Browser-Based Installation**
<img src="90. osTicket installed.png" width="80%" alt="Installation Complete"/>

Complete the osTicket installation and verify successful setup.

---

### **Step 16: Verify End-User Portal**
<img src="91. Support center_Support ticket system .png" width="80%" alt="End User Portal"/>

Confirm the osTicket support portal loads and is ready to accept tickets.

---
