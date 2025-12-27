<p align="center">
  <img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1 align="center">osTicket Help Desk Deployment</h1>
<h2 align="center">Prerequisites & Installation on Azure</h2>

<h3 align="center">
Microsoft Azure Windows VM | IIS | PHP | MySQL
</h3>


<div align="center">
  
  ![Azure](https://img.shields.io/badge/Microsoft_Azure-0089D6?style=for-the-badge&logo=microsoft-azure&logoColor=white)
  ![IIS](https://img.shields.io/badge/IIS-5E5E5E?style=for-the-badge)
  ![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)
  ![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
  ![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)
  ![PowerShell](https://img.shields.io/badge/PowerShell-5391FE?style=for-the-badge&logo=powershell&logoColor=white)

</div>

---

## 📋 Project Overview

**Project Type:** Infrastructure Deployment & Application Implementation  
**Status:** Complete and fully operational  
**Business Use Case:** A cloud-based help desk system to manage IT support requests efficiently  

This project shows a full deployment of **osTicket**, an open-source help desk platform, running on **Microsoft Azure**. The setup involved creating a Windows-based Azure Virtual Machine, configuring IIS with PHP, setting up a MySQL database, and testing the system through both end-user and administrator workflows.  

The project demonstrates practical skills in cloud infrastructure, web server setup, and help desk system management, reflecting a real-world IT support environment.

---

## 🖥️ Environments & Technologies Used

- Microsoft Azure (Virtual Machines)
- Windows 11 Pro (Azure VM)
- Internet Information Services (IIS) with CGI
- PHP 7.3
- MySQL 5.5
- Remote Desktop Protocol (RDP)
- PowerShell (administration & validation)

---

## ⚙️ osTicket Prerequisites

Before installing osTicket, the following components were required and configured:

1. Azure-hosted Windows Virtual Machine
2. IIS web server with CGI enabled
3. PHP runtime configured and registered in IIS
4. MySQL database server for ticket storage
5. Required PHP extensions (IMAP, Intl, OPcache)
6. Proper file permissions and security configuration

---

## 🛠️ Installation & Configuration Steps

<p>
  <img src="vm.png" width="80%" alt="Azure VM Creation"/>
</p>
<p>
Deployed a Windows 11 Pro virtual machine in Azure and connected via Remote Desktop to perform all installation and configuration tasks.
</p>

<br />

<p>
  <img src="IIS & PHP Configuration.png" width="80%" alt="IIS and PHP Configuration"/>
</p>
<p>
Configured IIS with CGI, registered PHP, and enabled required extensions for osTicket.
</p>

<br />

<p>
  <img src="osTicket installed.png" width="80%" alt="osTicket Installation"/>
</p>
<p>
Deployed osTicket to IIS, configured the database, completed installation, and verified operation.
</p>

---
