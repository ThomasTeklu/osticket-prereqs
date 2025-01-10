<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>

This is the first in a series of three repositories which will guide one through the process of creating an online ticketing system, akin to those used by various corporations/organizations to receive and resolve any issues that customers or internal members may file for assistance. In this first part, I will walk through how to spin up a virtual environment (Azure), establish and configure a web server, and enabling necessary parameters for the desired ticketing system (osTicket). 




<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computing/Networks & IP Addresses)
- Remote Desktop
- Internet Information Services (IIS)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Summary List of Prerequisites</h2>

- Web Server Configuration
- Website Configuration

<h1> 
  
# Web Server Configuration

### Virtual Machines

For setting up our ticketing system, we will be utilizing Microsoft Azure for virtual machines and computing. The Azure environment will serve as our construction grounds for building up and configuring the infrastructure of the ticketing system. 

Within Azure, create a new virtual machine specifying Windows OS, and 4 virtual CPUs; the rest of the default settings can be left as they are. This will serve as your main interface for setting up your osTicket system. Make sure to keep track of Administrator Account credentials as they will be frequently used throughout this three-part tutorial.

The creation of any virtual machine within Azure will come with a few attached components (IP address, Virtual Network, etc). 

![image](https://github.com/user-attachments/assets/0507bf09-9b66-4f8a-a6de-3996b51c1745)

<br />

These will automatically be sorted into a single "resource group" which will make administration of the VM (virtual machine) and its associated resources easier.

### Enabling Necessary Functionalities 

After the resources have been generated, log into the virtual machine by way of remote desktop, using the credentials you esablished. Within the VM, download the [Initial Installation Files](https://drive.google.com/uc?export=download&id=1b3RBkXTLNGXbibeMuAynkfzdBC1NnqaD) and unzip into your desktop. The folder should be called "osTicket-Installation-Files"

![image](https://github.com/user-attachments/assets/b8b6b4e1-31d0-49d2-a980-776fd2ad1d25)

We'll leave that there for now and return to it later.

You'll now turn this virtual machine into a web server. Open the Control Panel and navigate to "Programs" -> "Turn Windows features on or off". Then scroll down to "Internet Information Services" (IIS) and click the box next to it so that it displays a dark block mark within:

![image](https://github.com/user-attachments/assets/92d34843-5e9c-4e35-969d-b8e17d6c9c45)


Expanding the sub folders (clicking the small plus next to aforementioned box), navigate to "Web Wide Web Services" -> "Apllication Development Features" and click on the box next to the "CGI" feature:

![image](https://github.com/user-attachments/assets/7e941389-cad9-4155-afa7-8c7481d60e6f)


Installation/Enabling of the IIS functionality is absolutely crucial for any web server running on Windows OS since, it is the web server software itself: the nexus for receiving & processing requests from clients, as well as serving back the requested content. 

CGI (Common Gateway Interface) on the other hand is the protocol which web servers utilize to interact with external programs and scripts in order to generate dynamic content (processing input, accessing databases, etc.) in response to certain types of client requests.

<br />

# LEFT OFF HERE

Next, you'll open the "osTicket-Installation-Files" folder and install a variety of components necessary for successful operation and configuration of the web server. Start with the PHP Manager IIS (PHPManagerForIIS_V1.5.0.msi). When lanching the installer, select "Next" and "Allow" for any pages that follow.

![image](https://github.com/user-attachments/assets/890ab571-07e2-4571-a81e-5f179cce48bf)

Remaining in the same folder, install the Rewrite Module (rewrite_amd64_en-US.msi):

![image](https://github.com/user-attachments/assets/7933e578-eccb-4160-8aa6-c72fd13df5f3)

Returning to PHP, create a directory within the File Explorer named "C:\PHP":

![image](https://github.com/user-attachments/assets/59634676-e788-4f75-8ed8-a7c36060bbbb)

From the “osTicket-Installation-Files” folder, unzip PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) into the “C:\PHP” folder:

![image](https://github.com/user-attachments/assets/5aa16b46-8310-49a3-83a9-5caf5902ec6b)

Next, from the Installation Files folder, install VC_redist.x86.exe.



<br /> 
<br />
<br />

You'll now install your database server which is a crucial aspect for websites, especially for those which deal with dynamic-content generation which a ticketing system certainly will. Click on "mysql-5.5.62-win32.msi" to install MYSQL 5.5.62. Make sure to select "Typical" for "Choose Setup type" when prompted:

![image](https://github.com/user-attachments/assets/23b91a32-e795-4dd5-9b61-86203ece8e6f)

In addition to that, before selecting "Finish" ensure that "Launch the MySQL Instance Configuration Wizard":

![image](https://github.com/user-attachments/assets/7589a050-0fdd-4f12-b67c-d9490d309d2b)

You'll automatically be shown the aforementioned wizard. When prompted, select "Standard Configuration" then continue with the configuration:

![image](https://github.com/user-attachments/assets/a8c20f91-e281-452c-aba9-dba81c14ff0b)

Continue with standard settings. Make sure to set a root password that you will remember as it will be needed later on for establishing your database to work with your website later on:

![image](https://github.com/user-attachments/assets/d4ec0f24-e368-406e-a520-66486fbe40a8)

After all of this, select "Execute" to complete the configuration, then select "Finish".

<br />
<br />
<br />

# Website Configuration

With the parameters for a function web server now established, let's move on to more of the website-configuration side of things.

<br />

Open Internet INformation Services (IIS) Manager as an admin:

![image](https://github.com/user-attachments/assets/b9a9b32d-97a9-43ec-8e0c-974dc074ee7d)

Next, navigate to your website on the right-side pane, then select the "PHP Manager":

![image](https://github.com/user-attachments/assets/cb0d362a-b7ea-46b9-86fe-a82d1e86d582)

In the ensuing window, register the php-cgi.exe file that we located in our C:\PHP directory earlier. To do this click on "Register new PHP version" under the "PHP Setup" section. From there, link to the php file location on your drive. For a video demonstration, click on **the image directly below**:

[![Video Thumbnail](https://github.com/user-attachments/assets/0c698fd1-aa7f-41d1-b94a-ac131a23cd5e)](https://i.imgur.com/zIMlpOV.mp4)

Since the ticketing system will take in a lot of variable information, a server-side script that manages dynamic-content generation is essential.

You'll need to "reload" IIS here, so go ahead and renavigate to the osTicketVM Home, then hit "stop" and after "start" on the right-side panel:

![image](https://github.com/user-attachments/assets/854ed0b8-4782-4626-b5eb-0e5c33b2128a)

With that, you've gotten throught the "peripheral" settings. Let's now move on to the main part of this walkthrough: setting up the ticketing system itself.

### osTicket

Install osTicket v1.15.8 from the Installation Files folder by unzipping "osTicket-v1.15.8.zip". Copy the "upload" folder into "c:\inetpub\wwwroot". This is the directory wherein the material presentable to the client (i.e. the website) resides.

Within the wwwroot folder, rename the copied "upload" folder "osTicket":

![image](https://github.com/user-attachments/assets/f0b9d107-e351-46ef-8480-76b6e82e368f)

Return to IIS and reload again (stop and start the server). Underneath the "Default Web Site" section in the left-side panel, you should now see "osTicket". If you click on the expand option, you will see all the different types of files, images, scripts, and other components that comprise your website.

Click on "osTicket", the on the right-hand side select "Browse*.80". This will open your website:

![image](https://github.com/user-attachments/assets/1d79c1ae-4938-4c11-825d-8492b75c290f)

Notice the "Required" components that we installed earlier in our web server configuration section. Towards the bottom, you will notice that some of the "Recommended" extensions are not enabled. To enable these, we'll return to IIS, then the PHP Manager. Scroll down to the "PHP Extensions" and click "Enable or disable and extension:

![image](https://github.com/user-attachments/assets/18eb5370-8f95-4130-be79-c67ae469ceb0)

Locate the following within the disabled list, then right-click on them and select "Enable":

- php_imap.dil
- php_intl.dll
- php_opcache.dil

Now refresh the osTicket site within the browser and notice what changes.

<br />
<br />
<br />

Return to the File Explorer and open up your C drive. Within, rename: ost-config.php from "ost-sampleconfig.php" to "ost-config.php". Now right-click on that same file and select "Properties". Move to the "Security" tab and select the "Advanced" option. 

Within the newly openned window, select "Disable inheritance" then "Remove all inherited permissions from this object":

![image](https://github.com/user-attachments/assets/1678028b-aa0a-426f-91d9-30ded8ab76bf)

Now give permissions to everyone by selecting "Add" then "Select a principal" and finally entering in "Everyone" within the object name section. Make sure that these permissions are full by selecting "Full control" in the following window: 

![image](https://github.com/user-attachments/assets/c1a64e15-792c-4950-82af-fa5f164bbc5c)

Make sure to select "Apply" before clicking "OK" to close out of this section. 

<br />
<br />
<br />

Let's finish up the website setup.

Return to the browser and select "Continue". Give your Helpdesk a name and an email that will receive emails from "customers". In addition to this, establish Admin User credentials. 

Before moving on further in the browser, we're going to return one last time to the Installation Files folder. Install HeidiSQL.

**Note:** What we're installing now is not the database server itself as we installed that earlier. This rather, is a database management tool that allows for interaction with the database through a GUI. 

Continuing, open HeidiSQL and select "New" in the bottom left corner to create a new session:

![image](https://github.com/user-attachments/assets/64c42774-bb76-4e2a-950b-0140558b30a4)

Recall the MySQL password that you established earlier on, then enter that within the "Password" field. Next click "Open" and in the "Unnamed" pane, right-click in a blank space to create a databse and name it "osTicket":

![image](https://github.com/user-attachments/assets/4d0a6c31-500d-4898-a1fc-c2b33e6ac517)

Your database has now been created so now we can configure the website to use it. Return back to the browser and within the "Database Settings" section we left off on, enter in the Database name, MySQL Username (root), and the MySQL Password you selected. Click "Install Now" and congratulations!

If all went well, you should have your ticketing site completely setup and ready for use:

![image](https://github.com/user-attachments/assets/337d0711-54b0-49c8-89eb-335e919d1a7e)

Take note of the "Your osTicket URL" and "Your Staff Control Panel" as we will be utilizing them in the next installations of this walkthrough series. 

As the very last steps for this section, we'll do a bit of cleaning up. First, delete C:\inetpub\wwwroot\osTicket\setup. Next and lastly, change the permissions of the ost-config.php file we tinkered with earlier to "Read" only. Do this by again navigating to the file, opening its properties, clicking "Advanced" then double-click on "Full Control" and deselct every option except "Read". Apply the changes and exit.

In the next walkthrough, we'll work on Post-Installation Setup.


Until then, take care!


