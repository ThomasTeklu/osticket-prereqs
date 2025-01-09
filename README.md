<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>

This is the first in a series of three repositories which will guide one through the process of creating an online ticketing system, akin to those used by various corporations/organizations to receive and resolve any issues that customers or internal members may have. In this first part, I will walk through how to spin up a virtual environment (Azure), establish and configure a web server, and enabling necessary parameters for the desired ticketing system (osTicket). 




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computing/Networks & IP Addresses)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Summary List of Prerequisites</h2>

- Web Server Configuration
- Website Configuration
  
 Create and Connect to Azure Virtual Machine
 Install/Enable IIS (with CGI)
 Install and Register PHP from within IIS
 Install Microsoft Visual C++ Redistributable
 Install and Configure MySQL
 Move Core Files into Web Content Directory
 Enable Relevant Extensions within osTicket
 Create SQL Database Session
 Set up osTicket Through Browser

<h1>Web Server Configuration</h1>

### Virtual Machines

For setting up our ticketing system, we will be utilizing Microsoft Azure for virtual machines and computing. The Azure environment will serve as our construction grounds for building up and configuring the infrastructure of the ticketing system. 

Within Azure, create a new virtual machine specifying Windows OS, and 4 virtual CPUs; the rest of the default settings can be left as they are. This will serve as your main interface for setting up your osTicket system. Make sure to keep track of Administrator Account credentials as they will be frequently used throughout the three-part series.

The creation of any virtual machine within Azure will come with a few attached components (IP address, Virtual Network, etc). 

![image](https://github.com/user-attachments/assets/0507bf09-9b66-4f8a-a6de-3996b51c1745)

These will automatically be sorted into a single "resource group" which will make administration of the VM (virtual machine) and its associated resources easier.

### Enabling Necessary Functionalities 

After the resources have been generated, log into the virtual machine by way of remote desktop, using the credentials you esablished upon creation. Within the VM, download the [Initial Installation Files](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD) and unzip into your desktop. The folder should be called "osTicket-Installation-Files"

![image](https://github.com/user-attachments/assets/b8b6b4e1-31d0-49d2-a980-776fd2ad1d25)

We'll leave that there for now and return to it later.

You'll now turn this virtual machine into a web server. Open the Control Panel and navigate to "Programs" -> "Turn Windows features on or off". Then scroll down to "Internet Information Services" (IIS) and click the box next to it so that it displays a dark block mark within.

![image](https://github.com/user-attachments/assets/92d34843-5e9c-4e35-969d-b8e17d6c9c45)


Expanding the sub folders, navigate to "Web Wide Web Services" -> "Apllication Development Features" and click on the box next to the "CGI" feature.

![image](https://github.com/user-attachments/assets/7e941389-cad9-4155-afa7-8c7481d60e6f)


Installation/Enabling of the IIS functionality is absolutely crucial for any web server running on Windows OS since, first and foremost, it is the web server software itself, the nexus for receiving & processing requests from clients, as well as serving back the requested content. 

CGI (Common Gateway Interface) on the other hand is the protocol which web servers utilize to interact with external programs and scripts in order to generate dynamic content (processing input, accessing databases, etc.) in response to certain types of client requests.

<br />

Next, you'll open the "osTicket-Installation-Files" folder and install a variety of components necessary for successful operation and configuration of the web server. Start with the PHP Manager IIS (PHPManagerForIIS_V1.5.0.msi). When lanching the installer, select "Next" and "Allow" for any pages that follow.

![image](https://github.com/user-attachments/assets/890ab571-07e2-4571-a81e-5f179cce48bf)

Remaining in the same folder, install the Rewrite Module (rewrite_amd64_en-US.msi):

![image](https://github.com/user-attachments/assets/7933e578-eccb-4160-8aa6-c72fd13df5f3)

Returning to PHP, create a directory within the File Explorer named "C:\PHP":

![image](https://github.com/user-attachments/assets/59634676-e788-4f75-8ed8-a7c36060bbbb)

From the “osTicket-Installation-Files” folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the “C:\PHP” folder:

![image](https://github.com/user-attachments/assets/5aa16b46-8310-49a3-83a9-5caf5902ec6b)

Next, from the Installation Files folder, install VC_redist.x86.exe.

You'll now install MYSQL 5.5.62 (mysql-5.5.62-win32.msi)






# LATER

[![Video Thumbnail](https://github.com/user-attachments/assets/383629d3-37db-49e9-b3d9-b6e417db682e)](https://i.imgur.com/zIMlpOV.mp4)


From the Internet Information Services Manager, locate your website. Open the PHP Manager, then click on "Register new PHP version" under the "PHP Setup" section. From there, link to the php file location on your drive. For a video demonstration, click on **the image directly above**.

Since the ticketing system will take in a lot of variable information, a server-side script that manages dynamic-content generation is essential.


## SQL

![image](https://github.com/user-attachments/assets/adbaeb79-d946-4b6a-9af4-3df540a5360f)


![image](https://github.com/user-attachments/assets/f1da90da-9637-437e-a194-db5f4295178b)


![image](https://github.com/user-attachments/assets/d4332cc4-18b4-48f4-b127-08fd2b213511)


From the installation files folder, install MySQL server. Go through with a typical setup and configuration. Make sure to take note of the username and password that you establish as it will be needed later on for creating the website's database and linking it with the ticketing website itself.

## Making osTicket Accessible

![image](https://github.com/user-attachments/assets/fd8137cb-da0d-4d2a-a41b-e8325eb9374e)


Next, from the installation files folder, unzip the website (osTicket) files and transfer a copy of the "upload" folder to "c:\inetpub\wwwroot". After that, rename "upload" to "osTicket". 

You've now just made the files that your clients will be requesting (i.e. your website) available to them within your web server. c:\inetpub\wwwroot is the web server's default root directory for its front-side material; therefore renaming the "upload" folder to "osTicket" now gives the application its desired path that will be seen within the URL for those accessing the ticketing system.  


## Enabling Extensions

![image](https://github.com/user-attachments/assets/7870ed5e-6767-440a-b585-9af78aa1fe6a)


After reloading IIS (opening IIS, stopping and starting the server), open your site by navigating to it within IIS and clicking "Browse *:80". Pay attention to the fact that some extensions are not yet enabled. Go again then to your site with IIS, click on PHP Manager, then select "Enable or disable an extension". By right-clicking on, then selecting "enable", enable the following extensions:

1. php_imap.dil
2. php_intl.dil
3. php_opcache.dil

Refresh the osTicket site within the browser and see the changes that have ensued. 

## Creation of SQL Database Session

![image](https://github.com/user-attachments/assets/7c742ee8-fb2f-4e7d-9262-0f17fc2ce0ca)


![image](https://github.com/user-attachments/assets/7f092bfa-79e8-4fe7-a2b9-0223e7b2917f)


![image](https://github.com/user-attachments/assets/5b0e091a-3aa0-4c2e-8703-6cf5374d8c25)


Returning to the installation files folder, install HeidiSQL. Upon installation, open Heidi SQL and create a new session (here is where the MySQL credentials will come into use). From within the session, create a databse called "osTicket".

This step establishes the SQL database that the ticketing application will utilize to store and manage data. Heidi SQL itself is a graphical interface tool used for interacting with SQL databases, cutting out the need for a continous stream of commandline entries.

## Finishing Setup

![image](https://github.com/user-attachments/assets/36bfa859-de47-4f22-9db2-f374d6f89f03)


Finally, complete the settup of osTicket within the browser, establishing such things as your helpdesk username and password, admin account credentials, default email, etc. In addition to this, fill out the sections underneath "Database Settings" according to the database name and MySQL information previously established. If all is completed, your site should be up and running. The following page can be expected to be seen afterwards:


![image](https://github.com/user-attachments/assets/189e163a-2bfb-4fff-8e36-d35b7b2f5dfa)


### Next

Congratulations! You've just setup an osTicket system on your server and are now ready to put it to use. 








