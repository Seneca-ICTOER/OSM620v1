---
id: lab1
title: Lab 1 - Environment Setup
sidebar_position: 1
description: TBD
---

# Lab 1 - Environment Setup

## Investigation 1: Downloading Installation Media

In this investigation, you will be downloading your Windows OS installation media by logging into your Seneca-based Azure account. You will also be generating your personal serial keys.

1. Navigate to the Microsoft Azure site: portal.azure.com
2. Use your Seneca e-mail address and password to login.
3. Once on the main Azure page, look for the Search bar at the top of the page.
4. In the Search bar, type: Education, then hit Enter.
5. In the Education | Overview page, look to the left. You will see menu items already displayed on screen. (Overview, Learning resources, etc.)
6. Inside Learning resources in the left menu, click on Software.
7. In the main Software page, there is a Search bar just below the word Software (it says *Search* inside it.)
8. In that search field, type and enter: Windows Server 2025 Datacenter
9. In the item that appears below (there should only be one), click the link for Windows Server 2025 Datacenter.
10. On the right, an information box appears describing the software. Using your mouse to hover over this information box, scroll down to the bottom.
11. You should now see two items: **View Key** and **Download**
12. Click on **Download** first to begin downloading the Server 2025 ISO. You will need this for your operating system installation. (Don't forget where you've saved it!)
13. While the ISO file is downloading, click on **View Key**.
14. Copy this key into a text file that you save locally on your personal computer or personal USB key. You will need this for the Server installation and for any reinstalls later in the semester. **Do not lose this key and do NOT share it with anyone!**

## Investigation 2: VMWare Workstation

The use of VMware Workstation is required for this course. You can either use a Seneca Lab computer (Option 1) or a personal computer (Option 2). If you use an external SSD, you can use both!

**WARNING: Seneca Lab computers erase any saved data when restarted from their local drive. Save all work to an external drive or online storage.**

### Option 1a: Seneca Lab Computers w/VMware Workstation Installed Locally

How do you know if your particular Seneca Lab classroom has VMware Workstation installed?

**When you log in, the VMware Workstation icon will be visible on the desktop.** If it is not, jump to *Option 1b*.

1. Log in to the Seneca workstation with your Seneca username (don't include @myseneca.ca) and password.
2. Once the desktop has fully loaded, double-click on the **VMware Workstation** icon on the desktop. (If not present, jump to *Option 1b* instructions.)
3. When the **VMware Workstation** application appears on screen, continue to the next Investigation.

### Option 1b: Seneca Lab Computers *without* VMware Workstation Installed

**Do not use this option if your lab computer already has *VMware Workstation* installed. Go back to *Option 1a*.**

1. Log in to the Seneca workstation with your Seneca username (don't include @myseneca.ca) and password.
2. Once the desktop has fully loaded, double-click on the **Seneca MyApps** icon on the desktop.
3. In the browser that launches, log in with your Seneca credentials.
4. Do not ignore dialog boxes! Read them carefully instead of just clicking *Cancel* or randomly.
5. In the search bar in the middle of the screen, type *VMware* and hit **Enter.**
6. One result should show up, **VMware WS Pro**. Click this result.
7. In the new *VMware WS Pro* page, click on the version number (Example: 17.6.1). This will launch the application over the network.
8. Click on allow for any dialog boxes that appear. Remember, **do not ignore dialog boxes!**
9. Be patient. It can take a bit for the background files to transfer over the network.
10. When complete, the **VMware Workstation** application should appear on screen. (You will also see the **VMware Workstation** icon on the desktop. You can launch it from here if you accidentally close the program.)
11. Proceed to the next investigation.
### Option 2: Personal Computer

#### Part 1: Computer Hardware Requirements

To run this course and its tech on a personal computer, it must meet the following minimum system requirements:
1. CPU: 4-core Intel/AMD (2012 or later)
2. RAM: 16 GB
3. Storage: 250 GB SSD free, *reserved for this course* (if external, USB3.0 or higher)
4. Internet connection: High speed, stable

**CPU architecture is vital. You cannot use ARM or SnapDragon based computers. This includes all Apple Silicon computers (M1/M2/M3/M4, etc).**

#### Part 2: Registering Your Broadcom Account

Broadcom (formerly VMware) now requires account registration before you can download the VMware Workstation software. Follow the instructions below to do so. You only have to do this once. (If you already have an account using your Seneca e-mail, skip to Step 3.)

1. Visit the Broadcom registration site: https://profile.broadcom.com/web/registration
2. Provide your Seneca e-mail address and continue.
3. You will be sent a verification code. Check your Seneca e-mail and enter the code on the page.
4. On the *Complete your Registration* page, enter your information and click **Create Account.**
5. On the *Registered Successfully!* page, you can skip the rest and simply click **I'll do it later**.
6. At the top right of the screen, click on the **Login** button. (No, you aren't logged in automatically. Yes, it's annoying.)
7. Enter your Seneca e-mail address as your username and the password you chose on Step 4 as your credentials.
8. When complete, you should see your name in the top right of the screen instead of *Login.* If not, attempt to log in again or ask for help.

### Part 3: Downloading VMware Workstation
1. Go to this link: https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Pro&freeDownloads=true
2. Click on **WMware Workstation Pro 17 for Windows**
3. Click on the highest version available. (17.6.3 as of last update)
4. On the next screen, click on the blue link inside *I agree to the Terms and Conditions* to open a new tab with their terms and conditions. Do not close this window.
5. Back in the previous window/tab that's still open, now click the checkbox for *I agree to the Terms and Conditions*.
6. Click on the little cloud icon next to the name of the download file.
7. Click the **Yes** button when the dialog box pops up.
8. In the *Trade Compliance and Download Conditions* screen, fill in the following school information:
	1. Address1: **1750 Finch Ave E**
	2. City: **North York**
	3. State/Province: **Ontario**
	4. Country: **Canada**
	5. Zip/Postal Code: **M2J 2X5**
9. ***Finally*** click on the cloud icon again to begin the actual download.
10. If you ever need to download the software again, you won't have to go through any of the registration mess. Follow Part 3, Steps 1-3, then Step 9.
11. Direct link: https://downloads2.broadcom.com/?file=VMware-workstation-full-17.6.3-24583834.exe&oid=38988096&id=yvNR4Ur3i4n6Ic4Z3pGm4ZNuhcOR9OzqJ5c71zWGQWtt7jgem-_11MXlHeTdyjW73tEfOS8fwGI=&verify=1750391577-zQ%2BZJXDvInv3EbAMve2m8vmVtcjOe%2Fk1IQv17jA69gA%3D

### Part 4: Install VMware Workstation (TBD)
1. Find the downloaded .exe file and run the installer.
2. Follow all prompts and install.
3. (Free for use option?)

### Part 5: Launch VMware Workstation (TBD)
1. Open VMware Workstation from your desktop or the Start Menu.
2. When asked, choose the Free option.
3. Proceed to the next Investigation.

## Investigation 5: VM1 Installation - Windows Server 2025 Datacenter

Name: srv1-cjohnson30
RAM: 4GB
CPU: 2 cores
Storage: 80 GB

### Part 1: Setup Instructions

1. In the main window, you should see a large + symbol icon titled **Create a New Virtual Machine**. Click it.
2. In the new dialog box, keep *Typical* selected and click the **Next** button.
3. On the next screen, *Guest Operating System Installation*, do the following:
	1. Select *Installer disc image file (ISO):*
	2. Now click **Browse**.
		1. Navigate to where you saved your ***Windows Server 2025 Datacenter**** downloaded ISO and select it.
	3. Once selected, the previous screen should now say *"Windows Server 2025 detected.* If it doesn't, you haven't selected the right file, or your download was corrupted. Ask for help.
	4. Click **Next**.
4. On the "Easy Install Information" screen, do the following:
	1. Paste in your serial key.
	2. Version of Windows to install: Select *Windows Server 2025 Datacenter*
	3. Personalize Windows:
		1. Full Name: Administrator
		2. Password (both fields): Select a strong password **you will remember**. You will use this same password for all VMs in this course.
	4. ***Do not select "Log on automatically"***.
	5. Click **Next**.
5. On the "Name the Virtual Machine" screen, do the following:
	1. Virtual machine name: srv1-*senecausername*
		1. For example, if my Seneca e-mail address is cjohnson30@myseneca.ca, then my Seneca username is *cjohnson30*. This would give me a VM name of *srv1-cjohnson30*.
	2. Location: If using an external SSD (like with our lab computers), click **Browse** and navigate to your external SSD.
		1. Create the following directory structure in your SSD: *OSM620 > Virtual Machines/srv1-cjohnson30*
		2. Select this new *srv1-cjohnson30* folder.
		3. Make sure you now see this change in the Location field. (Example: *Z:/OSM620/Virtual Machines/srv1-cjohnson30*)
	3. Click **Next**.
6. On the "Specify Disk Capacity" screen, do the following:
	1. Maximum disk size (GB): **80**
	2. Select *Split virtual disk into multiple files*.
	3. Click Next.
7. On the "Ready to Create Virtual Machine" screen, do the following:
	1. Click on **Customize hardware...**
8. On the new "Hardware" screen, do the following:
	1. Select *Memory*, and change the value to: **4096**
	2. Select *Processors*, and change:
		1. Number of processors: **2**
		2. Number of cores per processor: **1**
		3. Virtualize Intel VT-x/EPT or AMD-V/RVI: **Checked**
		4. Virtualize CPU performance counters: ***Unchecked***
		5. Virtualize IOMMU (IO memory management unit): **Checked**
	3. Select *Network Adapter* and confirm:
		1. *Connected at power on:* **Checked**
		2. *NAT*: **Checked**
	4. Click **Close**.
9. Back in the "Ready to Create Virtual Machine" screen, click **Finish**.
10. The virtual machine should launch.
11. If you get a dialog box about *Side channel mitigations*, check the box for *Do not show this hint again* and click **OK**.
12. Click **Close**.
13. Click on the big **Play** to turn on the virtual machine begin the OS installation. This may take some time.

### Part 2: Post-Installation Tasks

* Time Zone
* Name Change
* Windows Activation
* Updates
* Internet Connectivity Check w/IE
* Download and Install Firefox

## Investigation 6: VM2 Installation - Windows Server 2025 Core

Name: srv2-cjohnson30
RAM: 2GB
CPU: 2 cores
Storage: 36 GB

### Part 1: Setup Instructions

1. In the main window, you should see a large + symbol icon titled **Create a New Virtual Machine**. Click it.
2. In the new dialog box, keep *Typical* selected and click the **Next** button.
3. On the next screen, *Guest Operating System Installation*, do the following:
	1. Select *Installer disc image file (ISO):*
	2. Now click **Browse**.
		1. Navigate to where you saved your ***Windows Server 2025 Datacenter*** downloaded ISO and select it.
	3. Once selected, the previous screen should now say *"Windows Server 2025 detected.* If it doesn't, you haven't selected the right file, or your download was corrupted. Ask for help.
	4. Click **Next**.
4. On the "Easy Install Information" screen, do the following:
	1. Paste in your serial key.
	2. Version of Windows to install: Select *Windows Server 2025 Datacenter* ***(Core)***
	3. Personalize Windows:
		1. Full Name: Administrator
		2. Password (both fields): Select a strong password **you will remember**. You will use this same password for all VMs in this course.
	4. ***Do not select "Log on automatically"***.
	5. Click **Next**.
5. On the "Name the Virtual Machine" screen, do the following:
	1. Virtual machine name: srv2-*senecausername*
		1. For example, if my Seneca e-mail address is cjohnson30@myseneca.ca, then my Seneca username is *cjohnson30*. This would give me a VM name of *srv2-cjohnson30*.
	2. Location: If using an external SSD (like with our lab computers), click **Browse** and navigate to your external SSD.
		1. Create the following directory structure in your SSD: *OSM620 > Virtual Machines > srv2-cjohnson30*
		2. Select this new *srv2-cjohnson30* folder.
		3. Make sure you now see this change in the Location field. (Example: *Z:/OSM620/Virtual Machines/srv2-cjohnson30*)
	3. Click **Next**.
6. On the "Specify Disk Capacity" screen, do the following:
	1. Maximum disk size (GB): **80**
	2. Select *Split virtual disk into multiple files*.
	3. Click Next.
7. On the "Ready to Create Virtual Machine" screen, do the following:
	1. Click on **Customize hardware...**
8. On the new "Hardware" screen, do the following:
	1. Select *Memory*, and change the value to: **4096**
	2. Select *Processors*, and change:
		1. Number of processors: **2**
		2. Number of cores per processor: **1**
		3. Virtualize Intel VT-x/EPT or AMD-V/RVI: **Checked**
		4. Virtualize CPU performance counters: ***Unchecked***
		5. Virtualize IOMMU (IO memory management unit): **Checked**
	3. Select *Network Adapter* and confirm:
		1. *Connected at power on:* **Checked**
		2. *NAT*: **Checked**
	4. Click **Close**.
9. Back in the "Ready to Create Virtual Machine" screen, click **Finish**.
10. The virtual machine should launch.
11. If you get a dialog box about *Side channel mitigations*, check the box for *Do not show this hint again* and click **OK**.
12. Click **Close**.
13. Click on the big **Play** to turn on the virtual machine begin the OS installation. This may take some time.

### Part 2: Post-Installation Tasks


## Investigation 7: VM3 Installation - Windows 11 Client

Name: client-cjohnson30
Name: client1-cjohnson30
RAM: 4GB
CPU: 2 processors
Storage: 64 GB

### Part 1: Setup Instructions

In the main window, you should see a large + symbol icon titled **Create a New Virtual Machine**. Click it.
2. In the new dialog box, keep *Typical* selected and click the **Next** button.
3. On the next screen, *Guest Operating System Installation*, do the following:
	1. Select *Installer disc image file (ISO):*
	2. Now click **Browse**.
		1. Navigate to where you saved your ***Windows 11 Education*** downloaded ISO and select it.
	3. Once selected, the previous screen should now say *"Windows 11 x64 detected."* If it doesn't, you haven't selected the right file, or your download was corrupted. Ask for help.
	4. Click **Next**.
4. On the "Name the Virtual Machine" screen, do the following:
	1. Virtual machine name: client1-*senecausername*
		1. For example, if my Seneca e-mail address is cjohnson30@myseneca.ca, then my Seneca username is *cjohnson30*. This would give me a VM name of *client1-cjohnson30*.
	2. Location: If using an external SSD (like with our lab computers), click **Browse** and navigate to your external SSD.
		1. Create the following directory structure in your SSD: OSM620 > Virtual Machines
		2. Select this new Virtual Machines folder.
		3. Make sure you now see this change in the Location field. (Example: Z:/OSM620/Virtual Machines)
	3. Click **Next**.
5. On the "Encryption Information" screen, do the following:
	1. Select *Only the files needed to support TPM are encrypted.*
	2. Enter the same password as your other VMs in both fields.
	3. **Uncheck** the *Remember the password on this machine in Credentials Manager* option.
	4. Click **Next**.
6. On the "Specify Disk Capacity" screen, do the following:
	1. Maximum disk size (GB): **64**
	2. Select *Split virtual disk into multiple files*.
	3. Click **Next**.
7. On the "Ready to Create Virtual Machine" screen, do the following:
	1. Click on **Customize hardware...**
8. On the new "Hardware" screen, do the following:
	1. Select *Memory*, and change the value to: **4096**
	2. Select *Processors*, and change:
		1. Number of processors: **2**
		2. Number of cores per processor: **1**
		3. Virtualize Intel VT-x/EPT or AMD-V/RVI: **Checked**
		4. Virtualize CPU performance counters: ***Unchecked***
		5. Virtualize IOMMU (IO memory management unit): **Checked**
	3. Select *Network Adapter* and confirm:
		1. *Connected at power on:* **Checked**
		2. *NAT*: **Checked**
	4. Click **Close**.
9. Back in the "Ready to Create Virtual Machine" screen, click **Finish**.
10. The virtual machine should launch.
11. If you get a dialog box about *Side channel mitigations*, check the box for *Do not show this hint again* and click **OK**.
12. Click **Close**.
13. Click on the big **Play** to turn on the virtual machine begin the OS installation. This may take some time.

### Part 2:  Installation Options

1. Once the Windows 11 Setup screen appears:
2. On *Select language settings*, keep the defaults and click **Next**.
3. On *Select keyboard settings*, keep the defaults and click **Next**.
4. On *Select setup option*, do the following:
	1. Select *Install Windows 11*
	2. Check the box next to *I agree everything will be deleted, including files, apps, and settings*
	3. Click **Next**.
5. On the *Product key* page, enter your product key and click **Next**.
6. On *Applicable notices and license terms*, click **Accept**.
7. On *Select location to install Windows 11*, keep the defaults and click **Next**.
8. On *Ready to install*, click **Install**.
9. The Windows Installer will now install the OS. This may take some time, and the percentage may freeze at certain points. Be patient.
10. When the installer finishes, Windows 11 will start up and you will be launched into the First-Run Setup. Go to Part 3.

### Part 3:  First-Run Setup

1. On *Is this the right country or region?*, select **Canada** and click **Yes.**
2. On *Is this the right keyboard layout or input method?*, stick with the default and click **Yes**.
3. On *Want to add a secondary keyboard layout?*, click **Skip**.

Windows will now check for available updates from the Internet. If it finds any, it will install them automatically.

This process may take some time. Please be patient. Your VM may restart on its own.

### Part 4: Account Creation

Now that language/keyboard and installer updates have been applied, it's time to create your account.
1. On *Let's set things up for work or school*, select **Sign-in options**.
2. On this next screen, click on **Domain join instead**.
3. On *Who's going to use this device?*, enter your **Seneca username**, (*Not* your full name), then click **Next**.
4. On *Create a super memorable password*, enter the same password you've used for your other VMs and click **Next**.
5. Confirm it on the next screen and continue.
6. On *Now add security questions*, fill out three security questions, clicking **Next** after each.
7. On *Let Microsoft and apps use your location*, select **No**, then click **Accept**.
8. On *Find my device*, select **No**, then click **Accept**.
9. On *Send diagnostic data to Microsoft*, scroll down to select **Required only**, then click **Accept**.
10. On *Improve inking & typing*, select **No**, then click **Accept**.
11. On *Get tailored experiences with diagnostic data*, select **No**, then click **Accept**.

Windows will now check for *more* available updates. As before, if it finds any, it will install them automatically.

This process may take some time. Please be patient. Your VM may restart on its own.

Once complete, you will be presented with a login screen. Move to the next part to continue.

## Investigation 8: Post-Installation Tasks - Windows 11

In this investigation, we'll log in for the first time and run through several post-installation tasks both necessary and for user comfort.

### Part 1: First Login

1. Enter your password to login. First-login may take a few minutes as your profile is set up.

### Part 2: Installing VMware Tools

1. Once presented with the desktop, the very first thing we'll do is install the **VMware Tools** to integrate better with the application.
2. Outside of the VM window, way at the top of the actual VMware Workstation application, look for the **VM** menu item. (The order at the top is *File*, *Edit*, *View*, *VM*, *Tabs*, *Help*, if you're having trouble finding it.)
3. Click the following: **VM** > **Install VMware Tools**
4. Ignore the "AutoPlay" dialog box that pops up. It can take a while and disappears quickly.
5. Instead, open the **Start Menu**, and click on **File Explorer**.
6. In the new File Explorer window, look to the left-side menu bar.
7. Scroll down to *DVD Drive* and click it.
8. Inside *DVD Drive: VMware Tools*, find and double-click on the file: **setup64**
9. On the *User Account Control* dialog box that pops up, click **Yes**.
10. Wait for the installer to load.
11. On the first screen of the installer, click **Next**.
12. On *Choose Setup Type*, select **Complete**, then click **Next**.
13. On *Ready to install VMware Tools*, click **Install**.
14. This may take a few minutes, and the screen may flash a few times.
15. When complete, the last screen has a **Finish** button. Click it. (You have no choice!)
16. The installer will then ask you if you'd like to restart your computer. Click **Yes**.

### Part 3: Setting the Time Zone

1. Login again.
2. Find the time on the bottom right of the screen (in the VM, not your host machine!)
3. Right-click on the time and select **Adjust date and time**.
4. Check the displayed time and time zone.
5. The time should match current time, and the time zone should say *"(UTC-5:00) Eastern Time (US & Canada)"*.
6. If the time zone is wrong, change it to the value above.
7. Confirm your time zone and time matches local time.

### Part 4: Setting Internal Computer Name

When we created our VM, we gave it the name *client1-SenecaUsername*. This only applies to how VMware Workstation sees the VM, not to how the internal Windows OS sees itself. We need to change that to match.

1. In the *Settings* window you still have open (or reopen it from the Search bar), look to the left-hand menu bar and select **System**.
2. The very first thing you see at the top is the current computer name. This is what we're going to change.
3. Click on the **Rename** text link.
4. In the *Name your device* field, enter your VM's name: **client1-SenecaUsername** (replacing *SenecaUsername* with your actual username)
5. Click **Next**.
6. You will now be asked if you'd like to restart. Click **Restart now**.
7. After restarting and logging back in, go into *Settings* > *System* and confirm your computer name is now **client1-SenecaUsername**.

### Part 4: Windows Updates

A critical part of a security-conscious mindset is running regular updates. **This is NOT something you do only once at the start of installation.** You should be running these regularly to keep up to date with security fixes and zero-day exploits.

1. If you're already in the *Settings* application, look through the left menubar for **Windows Update** and click it.
2. In the *Windows Update* main screen, scroll down to **Advanced Options** and click it.
3. The very first option is *Receive updates to other Microsoft products*. Toggle this from **Off** to **On**.
4. At the top of the screen, where it says *Windows Update > Advanced Options*, click **Windows Update** to go back to the previous screen.
5. You will likely already see updates ready. Click on **Download & install all**.
6. As you might expect, this can take a while. Timing will depend on your Internet connection, how fast your computer is, how fast your SSD is, and how many updates there are. Please be patient. Your computer may restart.
7. Once updates have begun, take a break while it does its thing. Grab a drink, make a sandwich, text a friend.
8. After updates are complete, go back into *Windows Update* and click **Check for updates** again. There may be (and often times are) more.
9. If there are more updates, complete Steps 5-8 again until there are no more updates available.
10. In *Windows Update*, scroll back down to **Advanced options** again and click it.
11. Inside *Windows Update > Advanced options* scroll down to **Optional updates** and click it.
12. Select all available updates that appear (you may have to expand some lists).
13. Click **Download & install**.

* Windows Activation
* Theme Changes (Dark Mode)
* Internet Connectivity Check w/IE
* Install Firefox and Make Default
* Slim Down Firefox and Change Search
* Remove Copilot

