<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>


<h1>osTicket - Prerequisites and Installation</h1>
This guide provides comprehensive instructions for setting up osTicket, an open-source ticketing system, on a Windows 10 environment hosted on Microsoft Azure. It covers the entire process from creating a virtual machine to configuring osTicket post-installation for handling ticket lifecycles.

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Preparation</h2> 

#### **Create an Azure Virtual Machine**

1. **Log into Azure Portal:**
   - Navigate to Virtual Machines and click on "Add"
   - Select your subscription and create a new resource group or choose an existing one
   - Choose a region (Make sure region is compatable with subsequent configuration steps)

2. **Configure VM:**
   - For the image, select Windows 10 Pro, Version 21H2
   - Size: Standard_DS2_v2 (or equivalent with 4 vCPUs)
   - Set up an administrator account (Username: `labuser`, Password: `chooseYourOwnPassword!` WRITE THIS DOWN!)
   - Allow RDP (Remote Desktop Protocol) on a public IP address for remote access

3. **Review and Create:**
   - Review your settings and click "Create"

#### **Connect to Your VM**

- Once the VM is deployed, connect via Remote Desktop using the public IP address and the credentials you set up

### **Installation**

#### **Step 1: Prepare the Environment**

1. **Install IIS:**
   - Open Control Panel → Programs → Turn Windows features on or off
   - Enable "Internet Information Services" with:
     - CGI
     - Common HTTP Features
     - IIS Management Console

2. **Create C:\PHP Directory:**
   - Navigate to C:\ and create a folder named: PHP
   - This will be used to store PHP installation files

#### **Step 2: Install Dependencies**

1. **Access Installation Files:**
   - Use the provided [Google Drive link](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6) to access and download the necessary installation files

2. **PHP Manager for IIS:**
   - Install `PHPManagerForIIS_V1.5.0.msi` from the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)

3. **Rewrite Module:**
   - Install `rewrite_amd64_en-US.msi` from the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)

4. **PHP 7.3.8:**
   - Download `php-7.3.8-nts-Win32-VC15-x86.zip` and extract it into `C:\PHP`
   - If prompted, choose to "Keep" the file

5. **Visual C++ Redistributable:**
   - Install `VC_redist.x86.exe` from the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6)

6. **MySQL 5.5.62:**
   - Install `mysql-5.5.62-win32.msi`from the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6) with a Typical Setup and configure it with the password `chooseYourOwnPassword!`

#### **Step 3: Configure IIS and PHP**

1. **Open IIS as an Administrator** and register PHP:
   - Use the PHP Manager in IIS to register the PHP version you've installed

2. **Reload IIS:**
   - Stop and then start the IIS server to apply changes

#### **Step 4: Install osTicket**

1. **Download osTicket v1.15.8** from the [Installation Files](https://drive.google.com/drive/u/1/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6) and extract the "upload" folder to `C:\inetpub\wwwroot`
   - Rename the "upload" folder to "osTicket"

2. **Reload IIS again** for changes to take effect

3. **Configure PHP Extensions in IIS:**
   - Navigate to your osTicket site settings in IIS and enable necessary PHP extensions (`php_imap.dll`, `php_intl.dll`, `php_opcache.dll`)

4. **Rename and Configure ost-config.php:**
   - Rename `ost-sampleconfig.php` to `ost-config.php` in `C:\inetpub\wwwroot\osTicket\include`
   - Adjust permissions:
     - Disable inheritance -> Remove All
     - New Permissions -> Everyone -> All

#### **Step 5: Finalize osTicket Setup**

1. **HeidiSQL for Database Management:**
   - Install HeidiSQL and create a new database named "osTicket" using the root account with the password `chooseYourOwnPassword!`

2. **Complete osTicket Setup:**
   - Access the osTicket setup page through your browser by navigating to `http://localhost/osTicket/setup`
   - Follow the on-screen instructions to configure your helpdesk, specifying the database details you just set up

3. **Cleanup:**
   - Delete the `C:\inetpub\wwwroot\osTicket\setup` directory
   - Set `ost-config.php` permissions to read-only

### **Conclusion**

Congratulations! You should now have a fully functional osTicket installation on your Windows 10 Azure VM. Access your help desk via `http://localhost/osTicket/scp/login.php` for the admin panel, and `http://localhost/osTicket/` for the user portal.

Remember, this tutorial assumes a certain level of familiarity with Azure, IIS, and web server administration. Adjustments might be needed based on your specific environment or osTicket version updates.
