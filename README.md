# osticket-prereqs
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.

# osTicket - Prerequisites and Installation

This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.

## Environments and Technologies Used
* Microsoft Azure (Virtual Machines/Compute)
* Remote Desktop
* Internet Information Services (IIS)

## Operating Systems Used
* Windows 10 (21H2)

## List of Prerequisites
* Enable IIS with CGI and Common HTTP Features
* PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)
* Rewrite Module (rewrite_amd64_en-US.msi)
* PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip)
* VC_redist.x86.exe
* MySQL 5.5.62 (mysql-5.5.62-win32.msi)

## Installation Steps

![1](https://github.com/user-attachments/assets/051cda8c-068d-4d33-bc24-76edfe7f5fba)


### Step 1: Create Virtual Machine in Azure
Create a new Virtual Machine (VM) in Microsoft Azure:
- Go to Azure Portal and click "Create a resource"
- Select "Virtual Machine"
- Choose Windows 10 Pro, Version 21H2
- Set VM size to Standard B2s (2 vcpus, 4 GiB memory)
- Create admin username and password
- Allow RDP (3389) in inbound port rules
- Review and create the VM

### Step 2: Connect to VM via Remote Desktop
- Copy the public IP address from your Azure VM
- Open Remote Desktop Connection on your local machine
- Enter the VM's public IP address
- Log in with the credentials you created

![Screenshot 2025-05-28 100354](https://github.com/user-attachments/assets/572c6f5b-be9b-409a-8a1f-e42cd84135cd)


### Step 3: Enable IIS in Windows
Within the VM, enable Internet Information Services:
- Open Control Panel → Programs → Turn Windows features on or off
- Check Internet Information Services
- Expand Internet Information Services → World Wide Web Services → Application Development Features
- Check CGI
- Expand Common HTTP Features and check all boxes
- Click OK and wait for installation to complete
- Test by opening a browser and navigating to 127.0.0.1 (should see IIS default page)

### Step 4: Download and Install PHP Manager for IIS
- Download PHPManagerForIIS_V1.5.0.msi from the web
- Run the installer and follow the setup wizard
- Accept license agreement and install to default location

### Step 5: Download and Install URL Rewrite Module
- Download rewrite_amd64_en-US.msi from Microsoft
- Run the installer with default settings
- This module is required for osTicket's clean URLs

![Screenshot 2025-05-28 100530](https://github.com/user-attachments/assets/a0334d00-790d-4167-a609-a3ef4f873219)

### Step 6: Create PHP Directory and Extract Files
- Create a new folder C:\PHP
- Download PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip)
- Extract all contents of the zip file into C:\PHP folder
- Note: Extract all files, not just the zip file itself

### Step 7: Install Visual C++ Redistributable
- Download and install VC_redist.x86.exe
- This provides necessary runtime components for PHP
- Follow the installation wizard with default settings

### Step 8: Install MySQL 5.5.62
- Download mysql-5.5.62-win32.msi
- Run installer and choose "Typical Setup"
- Launch Configuration Wizard after installation
- Select "Standard Configuration"
- Install as Windows Service and include Bin Directory in PATH
- Create root password (remember this password!)
- Execute configuration

![Screenshot 2025-05-28 100721](https://github.com/user-attachments/assets/819dc46b-033a-424c-8238-a7920a9150ab)

### Step 9: Configure PHP in IIS
Open IIS as Administrator:
- Open IIS Manager
- Click on PHP Manager
- Click "Register new PHP version"
- Browse to C:\PHP\php-cgi.exe
- Restart IIS server

### Step 10: Download and Install osTicket
- Download osTicket v1.15.8 from osTicket website
- Extract contents to C:\inetpub\wwwroot
- Rename "upload" folder to "osTicket"
- In IIS Manager, go to Sites → Default Web Site → osTicket
- On the right side, click "Browse *:80"

![Screenshot 2025-05-28 100827](https://github.com/user-attachments/assets/f3c8d697-d57f-4dbd-8ad5-3f1521ac5858)

### Step 11: Enable PHP Extensions
In IIS Manager, go to osTicket folder:
- Double-click PHP Manager
- Click "Enable or disable an extension"
- Enable the following extensions:
  - php_imap.dll
  - php_intl.dll
  - php_opcache.dll
- Refresh the osTicket site in browser to see changes

![Screenshot 2025-05-28 100956](https://github.com/user-attachments/assets/650e957a-dcfd-4c1f-8bb5-e6fdb79a1f8e)

### Step 12: Configure osTicket Settings
- Navigate to C:\inetpub\wwwroot\osTicket\include\
- Rename "ost-sampleconfig.php" to "ost-config.php"
- Right-click ost-config.php → Properties → Security
- Disable inheritance and remove all permissions
- Add new permissions for "Everyone" with Full Control

### Step 13: Complete osTicket Setup in Browser
Continue with osTicket setup in the browser:
- Fill out System Settings (Helpdesk Name, Default Email)
- Create Admin User account with username, password, and email
- Configure Database Settings:
  - MySQL Database: osTicket
  - MySQL Username: root
  - MySQL Password: (password created in Step 8)
- Click "Install Now"

### Step 14: Post-Installation Cleanup
After successful installation:
- Delete C:\inetpub\wwwroot\osTicket\setup folder
- Change permissions on C:\inetpub\wwwroot\osTicket\include\ost-config.php to "Read Only"
- Right-click file → Properties → Security → Advanced
- Remove "Everyone" and add appropriate permissions for IIS_IUSR

### Step 15: Test osTicket Installation
- Browse to your osTicket help desk: http://localhost/osTicket/
- Test admin panel: http://localhost/osTicket/scp/
- Create a test ticket to verify functionality
- Verify email notifications are working

## Congratulations!
You have successfully installed osTicket help desk ticketing system. The system is now ready to handle support tickets and can be customized further based on your organization's needs.
