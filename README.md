<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>






<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computing)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Summary List of Prerequisites</h2>

- Create and Connect to Azure Virtual Machine
- Install/Enable IIS (with CGI)
- Install and Register PHP from within IIS
- Install Microsoft Visual C++ Redistributable
- Install and Configure MySQL
- Move Core Files into Web Content Directory
- Enable Relevant Extensions within osTicket
- Create SQL Database Session
- Set up osTicket Through Browser

<h2>Installation Steps</h2>

![image](https://github.com/user-attachments/assets/4d0f26a5-9952-49e7-a047-ae3118a4be3d)

Creation of any virtual machine on Azure will come with a few attached components (IP address, Virtual Network, etc). Assorting within a single resource group makes tracking these much easier. 

<br />

![image](https://github.com/user-attachments/assets/57c12b65-f11d-4641-9b25-5819b4efb58a)


Open the Control Panel. From there, navigate to Programs->Turn Windows features on or off. Then, scroll down to "Internet Information Services" and turn it on. Within the sub folders, navigate to Web Wide Web Services->Apllication Development Features and turn on the "CGI" feature.

Installation/Enabling of the IIS functionality is absolutely crucial for any web server running on Windows OS since it is the nexus for receiving & processing requests from clients, interacting with dynamic-content generating componenets, and serving back the requested content. 

<br />

![image](https://github.com/user-attachments/assets/890ab571-07e2-4571-a81e-5f179cce48bf)


[![Video Thumbnail](https://github.com/user-attachments/assets/383629d3-37db-49e9-b3d9-b6e417db682e)](https://i.imgur.com/zIMlpOV.mp4)


From the Internet Information Services Manager, located your website. Open the PHP Manager, then click on "Register new PHP version" under the "PHP Setup" section. From there, link to the php file location on your drive. For a video demonstration, click on **the image directly above**.

Since the ticketing system will take in a lot of variable information, a server-side script that manages dynamic-content generation is essential.


![image](https://github.com/user-attachments/assets/adbaeb79-d946-4b6a-9af4-3df540a5360f)


![image](https://github.com/user-attachments/assets/f1da90da-9637-437e-a194-db5f4295178b)


![image](https://github.com/user-attachments/assets/d4332cc4-18b4-48f4-b127-08fd2b213511)


From the installation files folder, install MySQL server. Go through with a typical setup and configuration. Make sure to take note of the Username and Password that you establish as it will be needed later on for creating the website's database and linking it with the ticketing website itself.


![image](https://github.com/user-attachments/assets/fd8137cb-da0d-4d2a-a41b-e8325eb9374e)


Next, unzip the website files and transfer a copy of the "upload" folder into "c:\inetpub\wwwroot". After that, rename "upload" to "osTicket". 

You've now just made the files that your clients will be requesting (i.e. your website) available to them within your webserver. c:\inetpub\wwwroot is the web server's default root directory for their front-side material; therefore renaming the "upload" folder to "osTicket" now gives the application its desired path that will be seen within the URL for those accessing the ticketing system.  


![image](https://github.com/user-attachments/assets/7870ed5e-6767-440a-b585-9af78aa1fe6a)


After reloading IIS (Opening IIS, stopping and starting the server), open your site by navigating to it within IIS and clicking "Browse *:80". Pay attention to the fact that some extensions are not yet enabled. Go again then to your site with IIS, click on PHP Manager, then select "Enable or disable an extension". By right-clicking on, then selecting "enable", enable the following extensions:

1. php_imap.dil
2. php_intl.dil
3. php_opcache.dil

Refresh the osTicket site within the browser and see the changes that have ensued. 


![image](https://github.com/user-attachments/assets/7c742ee8-fb2f-4e7d-9262-0f17fc2ce0ca)


![image](https://github.com/user-attachments/assets/7f092bfa-79e8-4fe7-a2b9-0223e7b2917f)


![image](https://github.com/user-attachments/assets/5b0e091a-3aa0-4c2e-8703-6cf5374d8c25)


![image](https://github.com/user-attachments/assets/36bfa859-de47-4f22-9db2-f374d6f89f03)


![image](https://github.com/user-attachments/assets/189e163a-2bfb-4fff-8e36-d35b7b2f5dfa)












<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
