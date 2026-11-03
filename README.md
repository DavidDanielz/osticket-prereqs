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

### Step 1: Provision the Azure Virtual Machine

**Goal:** Create a Windows 11 VM in Microsoft Azure to host the osTicket environment.

**Procedure:**

1. Sign in to the [Azure Portal](https://portal.azure.com) and click **Create a resource**.
2. Search for **Virtual Machine** and click **Create**.
3. On the **Basics** tab, configure:
   - **Resource group:** `osticket-lab-rg` (create new)
   - **Virtual machine name:** `osticket-vm`
   - **Region:** `(US) East US`
   - **Image:** `Windows 11 Pro`
   - **Size:** `Standard_B2s` (2 vCPU, 4 GiB)
   - **Username:** `labadmin`
   - **Password:** (strong password, saved securely)
4. On the **Networking** tab, set **Inbound port rules** to allow **RDP (3389)**.
5. Click **Review + create** → **Create**. Wait ~3–5 minutes for deployment.
6. Confirm the VM shows **Running** on its overview page.

**Result:** The VM is provisioned and running in Azure.

![Azure VM created](images/step-01-azure-vm/step-01-azure-vm-created.png.png)

---

### Step 2: Connect via Remote Desktop

**Goal:** Establish an RDP session to the Azure VM so configuration can begin.

**Procedure:**

1. In the Azure Portal, open the `osticket-vm` overview page.
2. Click **Connect** → **RDP**.
3. Click **Download RDP File**.
4. Open the downloaded `.rdp` file.
5. When prompted, enter the VM credentials:
   - **Username:** `labadmin`
   - **Password:** (the password set during VM creation)
6. Accept the certificate warning if prompted (expected for a new VM).
7. Wait for the Windows desktop to load.

**Result:** An active Remote Desktop session showing the Windows 11 desktop of the Azure VM.

![Connected to VM via RDP](images/step-02-rdp/step-02-rdp-connected.png.png)

---

### Step 3: Download osTicket Installation Files

**Goal:** Obtain the osTicket package and extract it inside the VM.

**Procedure:**

1. Inside the RDP session, open Microsoft Edge.
2. Navigate to the osTicket releases page: `https://osticket.com/download/`.
3. Download the latest **osTicket v1.x** `.zip` package.
4. Once downloaded, right-click the `.zip` → **Extract All…**
5. Set the destination to `C:\osticket-install\` and click **Extract**.
6. Open the extracted folder and confirm you see the `upload` and `include` folders.

**Result:** The osTicket files are extracted locally on the VM, ready for deployment.

![osTicket installation files extracted](images/step-03-download/step-03-download-files.png.png)

---

### Step 4: Install IIS with CGI Enabled

**Goal:** Install Internet Information Services (IIS) with the CGI feature enabled so IIS can execute PHP.

**Procedure:**

1. Inside the RDP session, open **Server Manager**.
2. Click **Add roles and features**.
3. Click **Next** through the wizard until you reach **Server Roles**.
4. Check **Web Server (IIS)** → click **Add Features** when prompted.
5. Click **Next** through to **Role Services**.
6. Expand **Application Development** and check **CGI**.
7. Click **Next** → **Install**. Wait for the installation to complete.
8. Click **Close** when finished.

**Result:** IIS is installed with CGI enabled, ready to host PHP.

![IIS role selected in Server Manager](images/step-04-iis/step-04-iis-role-selected.png.png)

![CGI checked under Application Development Features](images/step-04-iis/step-04-iis-cgi-checked.png.png)

---

### Step 5: Install IIS Dependencies

**Goal:** Install PHP Manager for IIS and the IIS URL Rewrite Module — both required for osTicket to run correctly.

**Procedure:**

1. Inside the RDP session, download the **PHP Manager for IIS** installer.
2. Run the installer → **Next** → accept the license → **Install** → **Finish**.
3. Download the **IIS URL Rewrite Module 2** installer.
4. Run the installer → accept the license → **Install** → **Finish**.
5. Close and reopen **IIS Manager** (`inetmgr`) so the new modules load.
6. Confirm **PHP Manager** appears in the IIS Manager home page.

**Result:** Both dependencies are installed and PHP Manager is visible in IIS Manager.

![PHP Manager for IIS setup](images/step-05-iis-dependencies/step-05-php-manager-install.png.png)

![IIS URL Rewrite Module 2 setup](images/step-05-iis-dependencies/step-05-url-rewrite-install.png.png)

---

### Step 6: Install PHP Runtime

**Goal:** Install PHP 7.3.8 to `C:\PHP` so IIS can execute PHP scripts.

**Procedure:**

1. Inside the RDP session, create the folder `C:\PHP`.
2. Download the **PHP 7.3.8 (x64) Non-Thread-Safe** ZIP from `windows.php.net/downloads/releases/archives/`.
3. Right-click the ZIP → **Extract All…**
4. Set the destination to `C:\PHP` and click **Extract**.
5. Confirm `C:\PHP\php-cgi.exe` exists (this is the binary IIS will call).
6. Copy `php.ini-production` to `php.ini` in the same folder.

**Result:** PHP 7.3.8 is extracted to `C:\PHP` with a working `php.ini`.

![PHP 7.3.8 extracted to C:\PHP](images/step-06-php-runtime/step-06-php-extract.png.png)

---

### Step 7: Install Microsoft Visual C++ Redistributable

**Goal:** Install the Visual C++ Redistributable required by PHP and MySQL.

**Procedure:**

1. Inside the RDP session, download the **Microsoft Visual C++ Redistributable** installer (x64).
2. Run the installer.
3. Check **I agree to the license terms and conditions**.
4. Click **Install**.
5. Wait for setup to complete, then click **Close**.

**Result:** The Visual C++ Redistributable is installed, satisfying the runtime dependency for PHP and MySQL.

![Microsoft Visual C++ Redistributable installed](images/step-07-vcredist/step-07-vcredist-install.png.png)

---

### Step 8: Install MySQL Server

**Goal:** Install MySQL Server to serve as the backend database for osTicket.

**Procedure:**

1. Inside the RDP session, download the **MySQL Server 5.5** installer.
2. Run the installer and click **Next** through the welcome screen.
3. Accept the license agreement → **Next**.
4. Choose **Typical** setup type → **Install**.
5. Wait for installation to complete → **Next** → **Finish**.
6. When the configuration wizard launches, select **Standard Configuration** → **Next**.
7. Check **Install As Windows Service** (leave the default service name `MySQL`) → **Next**.
8. Set a **root password** (save it — needed later for HeidiSQL) → **Next** → **Execute**.
9. Click **Finish** once configuration completes.

**Result:** MySQL Server is installed, running as a Windows service, with a known root password.

![MySQL Server 5.5 installed](images/step-08-mysql/step-08-mysql-install.png.png)

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
