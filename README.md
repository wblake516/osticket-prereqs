<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Setup Guide</h1>
This guide outlines the steps required to set up the open-source help desk ticketing system, osTicket, including all necessary prerequisites.<br />


<h2>Technologies and Tools Utilized</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Protocol (RDP)
- Internet Information Services (IIS)

<h2>Operating System Used</h2>

- Windows 10 Pro (21H2)

<h2>Prerequisites</h2>

- An active Microsoft Azure account
- Basic familiarity with IIS (Internet Information Services)
- Access to Remote Desktop
- osTicket installation files
- HeidiSQL for database management

<h2>Table of Contents</h2>

- <a href="#create_vm">Create a Virtual Machine</a>
- <a href="#connect_vm">Connect to the Virtual Machine</a>
- <a href="#prepare_files">Prepare Installation Files</a>
- <a href="#enable_iis">Enable Internet Information Services</a>
- <a href="#install_files">Install Required Components</a>
- <a href="#setup_php">Set Up PHP</a>
- <a href="#setup_mysql">Install and Configure MySQL</a>
- <a href="#configure_iis">Configure IIS</a>
- <a href="#install_osticket">Install osTicket</a>
- <a href="#configure_osticket">Configure osTicket</a>
- <a href="#set_permissions">Set Permissions</a>
- <a href="#complete_setup">Finalize osTicket Setup</a>
- <a href="#install_heidisql">Install HeidiSQL</a>
- <a href="#verify_installation">Verify the Installation</a>

<h2>Setup Steps</h2>

<h3><a id="create_vm">1.) Create a Virtual Machine</a></h3>

- In Microsoft Azure, create a new virtual machine (VM) and a resource group called "osTicket".
- **VM Details:**
  - Name: osTicket-vm
  - OS Image: Windows 10 Pro, version 22H2 - 64-bit
  - Size: Minimum 2 vCPUs and 8 GB memory

<p>
<img src="https://i.imgur.com/JQf623y.png"/>
</p>

- Check the licensing agreement, then proceed to review and create the VM. No changes are needed for the management, disks, or networking options.

<p>
<img src="https://i.imgur.com/Y1eCwM2.png/img/">
</p>

<h3><a id="connect_vm">2.) Connect to the Virtual Machine</a></h3>

- Use the Remote Desktop Connection tool to log in to your VM.
- Enter the VM's public IP address and the login credentials you created during setup.

<p>
<img src="https://i.imgur.com/nzLIK8E.png/img"/>
</p>

<h3><a id="prepare_files">3.) Prepare Installation Files</a></h3>

- Within the VM, download the `osTicket-Installation-Files.zip` package.
- Extract the files to your desktop into a folder named `osTicket-Installation-Files`.

<p>
<img src="https://i.imgur.com/z08O4Wn.png"/>
</p>

<h3><a id="enable_iis">4.) Enable Internet Information Services</a></h3>

- Navigate to **Control Panel > Programs > Turn Windows features on or off**.
- Enable IIS and ensure the following components are selected:
  - **World Wide Web Services > Application Development Features > CGI**

<p>
<img src="https://i.imgur.com/LZAnWrt.png/img"/>
</p>
<img src="https://i.imgur.com/softeNW.png"/><h3><a id="install_files">
  
  5.) Install Required Components</a></h3>

- From the `osTicket-Installation-Files` folder:
  - Install **PHP Manager for IIS** using `PHPManagerForIIS_V1.5.0.msi`.
  - Install the **IIS Rewrite Module** using `rewrite_amd64_en-US.msi`.

<p>
<img src="https://i.imgur.com/softeNW.png/img"Installing IIS components"/>
</p>

<h3><a id="setup_php">6.) Set Up PHP</a></h3>

- Create a directory at `C:\PHP`.
- Extract the contents of `php-7.3.8-nts-Win32-VC15-x86.zip` into the `C:\PHP` directory.
- Run `VC_redist.x86.exe` to install the necessary runtime.

<p>
<img src="https://i.imgur.com/5zgJoW5.png"/>
<img src="https://imgur.com/zMDTDVk.png"/>
<img src="https://imgur.com/Nr55wrD.png"/>

<h3><a id="setup_mysql">7.) Install and Configure MySQL</a></h3>

- Use the `mysql-5.5.62-win32.msi` file to install MySQL.
- Select the **Typical Setup** option and complete the configuration wizard:
  - Choose **Standard Configuration**.
  - Set a username and password and save these credentials for later.

<p>
<img src="https://imgur.com/wa9O1Ub.png"/>
<img src="https://imgur.com/7kgVJAd.png"/>
<img src="https://imgur.com/481ulK8.png"/>

<h3><a id="configure_iis">8.) Configure IIS</a></h3>

- Open IIS as an administrator.
- Register PHP by navigating to **PHP Manager > Register PHP path** and selecting `C:\PHP\php-cgi.exe`.
- Restart IIS to apply the changes.

<p>
<img src="https://imgur.com/prNbPqY.png" alt="IIS configuration"/>
<img src="https://imgur.com/YbBolEh.png"/>
<img src="https://imgur.com/D8orsiT.png"/>
<img src="https://imgur.com/7VMnaxS.png"/>
</p>

<h3><a id="install_osticket">9.) Install osTicket</a></h3>

- Extract `osTicket-v1.15.8.zip` and copy the `upload` folder to `C:\inetpub\wwwroot`.
- Rename the `upload` folder to `osTicket` and restart IIS.

<p>
<img src="https://imgur.com/yy2u7aO.png"/> 
<img src="https://imgur.com/GDmtGWR.png"/>
<img src="https://imgur.com/G0yJbJP.png"/>
<img src="https://imgur.com/7VMnaxS.png"/> 
</p>

<h3><a id="configure_osticket">10.) Configure osTicket</a></h3>

- Open IIS, navigate to **Sites > Default > osTicket**, and click **Browse *:80**.
- Enable the following PHP extensions:
  - `php_imap.dll`
  - `php_intl.dll`
  - `php_opcache.dll`

<p>
<img src="https://imgur.com/1jxepHr.png" alt="PHP extensions"/>
<img src="https://imgur.com/USngp08.png"/>
<img src="https://imgur.com/4q4mQRL.png"/> 
</p>

<h3><a id="set_permissions">11.) Set Permissions</a></h3>

- Rename `ost-sampleconfig.php` to `ost-config.php` in the `C:\inetpub\wwwroot\osTicket\include` directory.
- Assign proper permissions by disabling inheritance, removing all permissions, and adding **Full Control** for **Everyone**.

<p>
<img src="https://imgur.com/RDi8vvR.png"/>
<img src="https://imgur.com/olfJtix.png"/>
<img src="https://imgur.com/NvWcxUt.png"/>
<img src="https://imgur.com/rgO3ZHr.png"/>
<img src="https://imgur.com/2p8vIIn.png"/>
<img src="https://imgur.com/fVLrmZF.png"/>
<img src="https://imgur.com/69aPyIZ.png"/>
<img src="https://imgur.com/zzxOkOI.png"/>
<img src="https://imgur.com/wX85FSX.png"/>
<img src="https://imgur.com/SsN9Jwn.png"/>
<img src="https://imgur.com/XKycyH8.png"/>
<img src="https://imgur.com/Qchtlgu.png"/>
</p>

<h3><a id="complete_setup">12.) Finalize osTicket Setup</a></h3>

- Complete the setup in your browser:
  - Set the help desk name.
  - Configure the default email address to receive support tickets.

<p>
<img src="https://imgur.com/8hGe90U.png"/>
<img src="https://imgur.com/oo1vWzC.png"/>
<
</p>

<h3><a id="install_heidisql">13.) Install HeidiSQL</a></h3>

- Install HeidiSQL from the installation files.
- Create a new session using the MySQL credentials and create a database named `osTicket`.

<p>
<img src="https://imgur.com/QXkWSx2.png"/>
<img src="https://imgur.com/z1P3oFn.png"/>
<img src="https://imgur.com/lVQtPm8.png"/>
<img src="https://imgur.com/6KkIwNy.png"/>
<img src="https://https://imgur.com/YKO13ej
<img src=">

<h3><a id="verify_installation">14.) Verify the Installation</a></h3>

- Access the osTicket help desk at:
  ```
  http://<your-vm-ip>/osTicket/scp/login.php
  ```

<p>
<img src="https://via.placeholder.com/800x400" alt="osTicket login"/>
</p>

<h2>Conclusion</h2>

Congratulations! You have successfully installed and configured osTicket on your virtual machine. Your help desk is ready for use.
