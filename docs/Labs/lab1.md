---
id: lab1
title: Lab 1 - Environment Setup
sidebar_position: 1
description: Lab 1 - Environment Setup
---

# Lab 1 - Environment Setup

## Investigation 1: Downloading Installation Media

In this investigation, you will be downloading your Windows OS installation media by logging into your Seneca-based Azure account. You will also generate your personal serial keys.

1. Navigate to the Microsoft Azure site: [portal.azure.com](https://portal.azure.com)
1. Use your Seneca e-mail address and password to login.
1. Once on the main Azure page, look for the Search bar at the top of the page.
1. In the Search bar, type: **Education**, then hit Enter.
1. In the **Education | Overview** page, look to the left. You will see menu items already displayed on screen. (*Overview*, *Learning resources*, etc.)
1. Inside **Learning resources** in the left menu, click on **Software**.
1. In the main **Software** page, there is a Search bar just below the word Software (it says *Search* inside it.)
1. In that search field, type and enter: **Windows Server 2025 Datacenter**
1. In the item that appears below (there should only be one), click the link for **Windows Server 2025 Datacenter**.
1. On the right, an information box appears describing the software. Using your mouse to hover over this information box, scroll down to the bottom.
1. You should now see two items: **View Key** and **Download**
1. Click on **Download** first to begin downloading the Server 2025 ISO. You will need this for your operating system installation. (Don't forget where you've saved it!)
1. While the ISO file is downloading, click on **View Key**.
1. Copy this key into a text file that you save locally on your personal computer or personal USB key. You will need this for the Server installation and for any reinstalls later in the semester. **Do not lose this key and do NOT share it with anyone!**

## Investigation 2: VMWare Workstation

The use of VMware Workstation is required for this course. You can either use a Seneca Lab computer (Option 1) or a personal computer (Option 2).

If you use an external SSD, you can use both!

**WARNING: Seneca Lab computers erase any locally saved data when restarted from their internal drives. Save all work to an external drive or online storage.**

### Option 1a: Seneca Lab Computers w/VMware Workstation Installed Locally

How do you know if your particular Seneca Lab classroom has VMware Workstation installed?

**When you log in, the VMware Workstation icon will be visible on the desktop.** If it is not, jump to *Option 1b*.

1. Log in to the Seneca workstation with your Seneca username (don't include @myseneca.ca) and password.
1. Once the desktop has fully loaded, double-click on the **VMware Workstation** icon on the desktop. (If not present, jump to *Option 1b* instructions.)
1. When the **VMware Workstation** application appears on screen, continue to the next Investigation.

### Option 1b: Seneca Lab Computers *without* VMware Workstation Installed

**Do not use this option if your lab computer already has *VMware Workstation* installed. Go back to *Option 1a*.**

1. Log in to the Seneca workstation with your Seneca username (don't include @myseneca.ca) and password.
1. Once the desktop has fully loaded, double-click on the **Seneca MyApps** icon on the desktop.
1. In the browser that launches, log in with your Seneca credentials.
1. Do not ignore dialog boxes! Read them carefully instead of just clicking *Cancel* or randomly.
1. In the search bar in the middle of the screen, type *VMware* and hit **Enter.**
1. One result should show up, **VMware WS Pro**. Click this result.
1. In the new *VMware WS Pro* page, click on the version number (Example: 17.6.1). This will launch the application over the network.
1. Click on allow for any dialog boxes that appear. Remember, **do not ignore dialog boxes!**
1. Be patient. It can take a bit for the background files to transfer over the network.
1. When complete, the **VMware Workstation** application should appear on screen. (You will also see the **VMware Workstation** icon on the desktop. You can launch it from here if you accidentally close the program.)
1. Proceed to the next investigation.

### Option 2: Personal Computer

#### Part 1: Computer Hardware Requirements

To run this course and its tech on a personal computer, it must meet the following minimum system requirements:

1. CPU: **6-core Intel/AMD** (ARM/M1 and Snapdragon will not work)
1. RAM: **32 GB**
1. Storage: **250 GB SSD free**, *reserved for this course* (if external, USB3.0 or higher)
1. Internet connection: **High speed, stable**

**CPU architecture is vital. You cannot use ARM or SnapDragon based computers. This includes all Apple Silicon computers (M1/M2/M3/M4, etc).**

#### Part 2: Registering Your Broadcom Account

Broadcom (formerly VMware) now requires account registration before you can download the VMware Workstation software. Follow the instructions below to do so. You only have to do this once. (If you already have an account using your Seneca e-mail, skip to Step 3.)

1. Visit the Broadcom registration site: profile.broadcom.com/web/registration
1. Provide your Seneca e-mail address and continue.
1. You will be sent a verification code. Check your Seneca e-mail and enter the code on the page.
1. On the *Complete your Registration* page, enter your information and click **Create Account.**
1. On the *Registered Successfully!* page, you can skip the rest and simply click **I'll do it later**.
1. At the top right of the screen, click on the **Login** button. (No, you aren't logged in automatically. Yes, it's annoying.)
1. Enter your Seneca e-mail address as your username and the password you chose on Step 4 as your credentials.
1. When complete, you should see your name in the top right of the screen instead of *Login.* If not, attempt to log in again or ask for help.

### Part 3: Downloading VMware Workstation

1. Go to this link: [Download VMware Workstation](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Pro&freeDownloads=true)
1. Click on **WMware Workstation Pro 17 for Windows**
1. Click on the highest version available. (17.6.3 as of last update)
1. On the next screen, click on the blue link inside *I agree to the Terms and Conditions* to open a new tab with their terms and conditions. Do not close this window.
1. Back in the previous window/tab that's still open, now click the checkbox for *I agree to the Terms and Conditions*.
1. Click on the little cloud icon next to the name of the download file.
1. Click the **Yes** button when the dialog box pops up.
1. In the *Trade Compliance and Download Conditions* screen, fill in the following school information:
    1. Address1: **1750 Finch Ave E**
    1. City: **North York**
    1. State/Province: **Ontario**
    1. Country: **Canada**
    1. Zip/Postal Code: **M2J 2X5**
1. ***Finally*** click on the cloud icon again to begin the actual download.
1. If you ever need to download the software again, you won't have to go through any of the registration mess. Follow Part 3, Steps 1-3, then Step 9.

### Part 4: Install VMware Workstation

1. Find the downloaded .exe file and run the installer.
1. Follow all prompts and install.

### Part 5: Launch VMware Workstation

1. Open **VMware Workstation** from your desktop or the Start Menu.
1. When asked, paste in your serial key.
1. Proceed to the next Investigation.

## Investigation 3: VM1 Installation - Windows Server 2025 Datacenter (*srv1*)

* Hypervisor: **VMware Workstation**
* Name: **srv1-cjohnson30**
* RAM: **16 GB**
* CPU: **6 cores**
* Storage: **250 GB**
* Networking: **2 NICs**

### Part 1: Setup Instructions

1. In the main window, you should see a large + symbol icon titled **Create a New Virtual Machine**. Click it.
1. In the new dialog box, keep *Typical* selected and click the **Next** button.
1. On the next screen, *Guest Operating System Installation*, do the following:
    1. Select *Installer disc image file (ISO):*
    1. Now click **Browse**.
    1. Navigate to where you saved your ***Windows Server 2025 Datacenter*** downloaded ISO and select it.
    1. Once selected, the previous screen should now say:

        > **Windows Server 2025 detected.**
        >
        > This operating system will use Easy Install.

    1. If it doesn't, you haven't selected the right file, or your download was corrupted. **Ask for help.**
    1. Click **Next**.
1. On the "Easy Install Information" screen, do the following:
    1. Paste in your serial key.
    1. Version of Windows to install: Select *Windows Server 2025 Datacenter*
    1. Personalize Windows:
        1. Full Name: **Administrator**
        1. Password (both fields): Select a strong password **you will remember**. You will use this same password for all VMs in this course.
        1. ***Do not select "Log on automatically"***.
        1. Click **Next**.
1. On the "Name the Virtual Machine" screen, do the following:
    1. Virtual machine name: **srv1-*senecausername***
       > **Explanation:** For example, if my Seneca e-mail address is `cjohnson30@myseneca.ca`, then my Seneca username is *cjohnson30*. This would give me a VM name of *srv1-cjohnson30*.
    1. Location: If using an external SSD (like with our lab computers), click **Browse** and navigate to your external SSD.
        1. Create the following directory structure in your SSD: *OSM620 > Virtual Machines/srv1-cjohnson30*
        1. Select this new *srv1-cjohnson30* folder.
        1. Make sure you now see this change in the Location field.

           > **Example:** *Z:/OSM620/Virtual Machines/srv1-cjohnson30*

    1. Click **Next**.
1. On the "Specify Disk Capacity" screen, do the following:
    1. Maximum disk size (GB): **250**
    1. Select *Split virtual disk into multiple files*.
    1. Click Next.
1. On the "Ready to Create Virtual Machine" screen, do the following:
    1. Click on **Customize hardware...**
1. On the new "Hardware" screen, do the following:
    1. Select *Memory*, and change the value to: **16384**
    1. Select *Processors*, and change:
        1. Number of processors: **1**
        1. Number of cores per processor: **6**
        1. Virtualize Intel VT-x/EPT or AMD-V/RVI: **Checked**
        1. Virtualize CPU performance counters: ***Unchecked***
        1. Virtualize IOMMU (IO memory management unit): **Checked**
    1. Select *Network Adapter* and confirm:
        1. *Connected at power on:* **Checked**
        1. *NAT*: **Checked**
    1. Click on the ***Add...*** button on the bottom left of the *Hardware* window.
        1. Select *Network Adapter* and click **Finish**.
        1. Back in the *Hardware* window, click on *Network Adapter 2*.
        1. Under *Network connection*, click the **Custom: Specific virtual network** radio button.
        1. Just below that, click the drop-down (it likely says *VMnet0* by default). Find and select **VMnet10**.
        1. Click **Close**.
1. Back in the "Ready to Create Virtual Machine" screen, click **Finish**.
1. The virtual machine should launch.
1. If you get a dialog box about *Side channel mitigations*, check the box for *Do not show this hint again* and click **OK**.
1. Your new Virtual Machine should now finish creating and then turn on and begin the OS installation.
1. Windows installation is automated at this point and won't require any input from you. It may restart several times.

    > **Time Note:** Installation may take some time.
    >
    > Feel free to get some caffeine or make a sandwich.

1. Eventually, you will be presented with the desktop and the VMware Tools installer having completed and asking if you'd like to restart. Choose **Yes**.
1. Once you've restarted, you're installation is complete.

## Investigation 4: Post-Installation Tasks (*srv1*)

After installing a new operating system, there are always a number of **post-installation tasks** to complete. **These aren't optional!**

### Step 1: Applying Time Zone Settings

This one is fairly straight-forward. Having the proper time zone set (EST) is essential for proper time keeping and ensuring encrypted webpages connect properly.

1. In the *Server Manager* application, click on **Local Server** in the left-hand menubar.
1. In the main *Properties* area, on the right-hand column, look for the *Time Zone* line. It should say **(UTC-05:00) Eastern Time (US & Canada)**.
1. If the *Time Zone* line item doesn't say the above, click on the displayed time zone and change it to UTC-05:00 as seen above.

### Step 2: Server Name Change

The default name applied to your new server will be semi-randomized. For proper identification (and to not wonder which server you're on when you have several), we're going to change this.

1. In the *Server Manager* application, click on **Local Server** in the left-hand menubar.
1. In the main *Properties* area, on the left-hand column, look for the *Computer name* line.
1. Click the current computer name.
1. In the *System Properties* dialog box that pops up, find the **Change** button and click it. (Ignore the *Computer Description* field. It's tempting, but wrong!)
1. In the new *Computer Name/Domain Changes* dialog box that pops up, find the *Computer name* field. Replace it with **srv1-SenecaUsername**.
1. When you click **OK**, the system will warn you about restarting. Choose to restart the system when asked.
1. Once you've restarted and logged back in, go back to the *Server Manager* from Step 1 and double-check your new computer name is correct. **Do not skip this step!**
1. If it is, you're done!

### Step 3: Windows Activation

Activating Windows unlocks certain settings and features. Since you've used your valid serial key (right?), you can activate with Microsoft easily.

1. In the *Server Manager* application, click on **Local Server** in the left-hand menubar.
1. In the main *Properties* area, on the right-hand column, look for the *Product ID* line.
1. Click on the **Not activated** link.
1. Follow the instructions in the popup dialog box. If unable to activate easily, **ask your professor for help**.

### Step 4: Installing OS Updates

A critical part of a security-conscious mindset is running regular updates. **This is NOT something you do only once at the start of installation.** You should be running these regularly to keep up to date with security fixes and zero-day exploits.

1. If you're already in the *Settings* application, look through the left menubar for **Windows Update** and click it. (Otherwise, click on the *Start* menu and search for **Updates**.)
1. In the *Windows Update* main screen, scroll down to **Advanced Options** and click it.
1. The very first option is *Receive updates to other Microsoft products*. Toggle this from **Off** to **On**.
1. At the top of the screen, where it says *Windows Update > Advanced Options*, click **Windows Update** to go back to the previous screen.
1. You will likely already see updates ready. Click on **Download & install all**.
1. As you might expect, this can take a while. Timing will depend on your Internet connection, how fast your computer is, how fast your SSD is, and how many updates there are. Please be patient. Your computer may restart.
1. Once updates have begun, take a break while it does its thing. Grab a drink, make a sandwich, text a friend.
1. After updates are complete, go back into *Windows Update* and click **Check for updates** again. There may be (and often times are) more.
1. If there are more updates, complete Steps 5-8 again until there are no more updates available.
1. In *Windows Update*, scroll back down to **Advanced options** again and click it.
1. Inside *Windows Update > Advanced options* scroll down to **Optional updates** and click it.
1. Select all available updates that appear (you may have to expand some lists).
1. Click **Download & install**.

### Step 5: Internet Connectivity Check w/Edge

We'll double-check we can access the Internet using the built-in Microsoft Edge application.

1. Open *Microsoft Edge*.
1. Go through the first-run questions.
1. When able, use the browser to navigate to **eff.org**.
1. If the website loads, move on to the next step. If not, **ask your professor for help**.

### Step 6: Download and Install Firefox

There are a ton of feature and privacy reasons *not* to use Microsoft Edge. Instead, we'll download and install **Mozilla Firefox** and use that going forward.

1. Open *Microsoft Edge*.
1. Navigate to: [Download Mozilla Firefox](https://www.firefox.com/en-CA/browsers/desktop/windows)
1. Wait for the installer to finish, then open it.
1. Follow the installer instructions.
1. Once complete, open *Firefox* and navigate to **eff.org** to check everything is okay.
1. Close *Microsoft Edge* forever.

## Investigation 5: VM2 Installation - Windows Server 2025 Core (*srv2*)

* Hypervisor: **VMware Workstation**
* Name: **srv2-cjohnson30**
* RAM: **4 GB**
* CPU: **2 cores**
* Storage: **250 GB**
* Networking: **2 NICs**

### Part 1: Setup Instructions

1. In the main window, you should see a large + symbol icon titled **Create a New Virtual Machine**. Click it.
1. In the new dialog box, keep *Typical* selected and click the **Next** button.
1. On the next screen, *Guest Operating System Installation*, do the following:
    1. Select *Installer disc image file (ISO):*
    1. Now click **Browse**.
       1. Navigate to where you saved your ***Windows Server 2025 Datacenter*** downloaded ISO and select it.
       1. Once selected, the previous screen should now say *"Windows Server 2025 detected.* If it doesn't, you haven't selected the right file, or your download was corrupted. Ask for help.
    1. Click **Next**.
1. On the "Easy Install Information" screen, do the following:
    1. Paste in your serial key.
    1. Version of Windows to install: Select *Windows Server 2025 Datacenter* ***(Core)***
    1. Personalize Windows:
       1. Full Name: Administrator
       1. Password (both fields): Select a strong password **you will remember**. You will use this same password for all VMs in this course.
    1. ***Do not select "Log on automatically"***.
    1. Click **Next**.
1. On the "Name the Virtual Machine" screen, do the following:
    1. Virtual machine name: **srv2-*senecausername***

       > **Explanation:** For example, if my Seneca e-mail address is `cjohnson30@myseneca.ca`, then my Seneca username is *cjohnson30*. This would give me a VM name of *srv2-cjohnson30*.
    1. Location: If using an external SSD (like with our lab computers), click **Browse** and navigate to your external SSD.
       1. Create the following directory structure in your SSD: *OSM620 > Virtual Machines > srv2-cjohnson30*
       1. Select this new *srv2-cjohnson30* folder.
       1. Make sure you now see this change in the Location field. (Example: *Z:/OSM620/Virtual Machines/srv2-cjohnson30*)
    1. Click **Next**.
1. On the "Specify Disk Capacity" screen, do the following:
    1. Maximum disk size (GB): **250**
    1. Select *Split virtual disk into multiple files*.
    1. Click Next.
1. On the "Ready to Create Virtual Machine" screen, do the following:
    1. Click on **Customize hardware...**
1. On the new "Hardware" screen, do the following:
    1. Select *Memory*, and change the value to: **4096**
    1. Select *Processors*, and change:
       1. Number of processors: **1**
       1. Number of cores per processor: **2**
       1. Virtualize Intel VT-x/EPT or AMD-V/RVI: **Checked**
       1. Virtualize CPU performance counters: ***Unchecked***
       1. Virtualize IOMMU (IO memory management unit): **Checked**
    1. Select *Network Adapter* and confirm:
        1. *Connected at power on:* **Checked**
        1. *NAT*: **Checked**
    1. Click on the ***Add...*** button on the bottom left of the *Hardware* window.
        1. Select *Network Adapter* and click **Finish**.
        1. Back in the *Hardware* window, click on *Network Adapter 2*.
        1. Under *Network connection*, click the **Custom: Specific virtual network** radio button.
        1. Just below that, click the drop-down (it likely says *VMnet0* by default). Find and select **VMnet10**.
        1. Click **Close**.
1. Back in the "Ready to Create Virtual Machine" screen, click **Finish**.
1. The virtual machine should launch.
1. If you get a dialog box about *Side channel mitigations*, check the box for *Do not show this hint again* and click **OK**.
1. Your new Virtual Machine should now finish creating and then turn on and begin the OS installation.
1. Windows installation is automated at this point and won't require any input from you. It may restart several times.

    > **Time Note:** Installation may take some time.
    >
    > Feel free to get some caffeine or make a sandwich.

1. Eventually, you will be presented with the desktop and the VMware Tools installer having completed and asking if you'd like to restart. Choose **Yes**.
1. Once you've restarted, you're installation is complete.

### Part 2: Post-Installation Tasks

## Investigation 4: Post-Installation Tasks (*srv2*)

After installing a new operating system, there are always a number of **post-installation tasks** to complete. **These aren't optional!**

### Step 1: Applying Time Zone Settings

This one is fairly straight-forward. Having the proper time zone set (EST) is essential for proper time keeping and ensuring encrypted webpages connect properly.

1. In the *SConfig* application, select Option 9 (*Date and Time*). Use your keyboard.
1. The *Date and Time* dialog box pops up.
1. Look for the *Time Zone* line. It should say **(UTC-05:00) Eastern Time (US & Canada)**.
1. If the *Time Zone* line item doesn't say the above, click on the *Change time zone...* button and change it to UTC-05:00 as seen above.
1. Click **OK* to close out of *Date and Time*.
1. Back in *SConfig*, choose Option 9 again to confirm your changes have stuck. If yes, continue to Step 2.

### Step 2: Server Name Change

The default name applied to your new server will be semi-randomized. For proper identification (and to not wonder which server you're on when you have several), we're going to change this.

1. In the *SConfig* application, selection Option 2 (*Computer name*). Use your keyboard.
1. In the new *Computer name* screen, enter your new computer name in the waiting text field: **srv2-SenecaUsername**
1. Press **Enter** on your keyboard to confirm the change.
1. The system now asks you about restarting. Enter **Y** to choose yes and hit the **Enter** key to confirm.
1. Once you've restarted and logged back in, go back to the *Computer name* screen from Step 2 and double-check your new computer name is correct. **Do not skip this step!**
1. If it is, you're done!

### Step 3: Windows Activation

Activating Windows unlocks certain settings and features. Since you've used your valid serial key (right?), you can activate with Microsoft easily.

1. In the *SConfig* application, select Option 11 (*Windows activation*). Use your keyboard.
1. In the new *Windows activation* screen, enter **2** (*Activate Windows*) and hit **Enter** to begin the activation process with Microsoft.
1. Follow the instructions on screen. If unable to activate easily, **ask your professor for help**.

### Step 4: Installing OS Updates

A critical part of a security-conscious mindset is running regular updates. **This is NOT something you do only once at the start of installation.** You should be running these regularly to keep up to date with security fixes and zero-day exploits.

1. In the *SConfig* application, select Option 5 (*Update settings*). Use your keyboard.
1. In the new *Update setting* screen, enter **5** (*Opt-in to Microsoft Update*) and hit **Enter** to confirm.
1. The next screen will ask you confirm again. Enter **y** and hit **Enter** to continue. (Then, hit **Enter** again.)
1. In the *SConfig* application, select Option 6 (*Install updates*). Use your keyboard.
1. In the new *Install updates* screen, enter **1** (*All quality updates*) and hit **Enter** to confirm.
1. After a short check, you are asked which updates to install. Select **a** to install all updates and hit **Enter** to confirm.
1. As you might expect, this can take a while. Timing will depend on your Internet connection, how fast your computer is, how fast your SSD is, and how many updates there are. Please be patient.
1. Once updates have begun, take a break while it does its thing. Grab a drink, make a sandwich, text a friend.
1. If asked to restart, choose **yes**.
1. After updates are complete, go through Steps 4-6 again. Do so until the system tells you there are no new updates. (It may take a few cycles to get them all.)
1. When complete, shut down *srv2*. Use the on-screen menu options in *SConfig* to do so.

### Step 5: Configuring Network Interface Card 2 (NIC2)

We have two network interfaces on this virtual machine. NIC1 is set to DHCP and is our Internet connection. We don't touch that one. It's configuration is automatic.

**However, NIC2 requires manual configuration.** Why do we need NIC2? It's what we'll be using to communicate with *srv1* and our other VMs.

1. In the *SConfig* application, select Option 8 (*Network Settings*).
1. In the *Network settings* screen, look for the unconfigured network adapater. It's likely the second one, and will likely have an address starting with **169.** If you aren't sure, ask your professor for help.
1. Select that adapter using the menu option and your keyboard, and hit **Enter** to confirm.
1. In the *Network adapter settings* screen, select Option 4 (*Rename network adapter*).
1. Enter the new network adapter name in the field: **Internal Network**
1. Hit **Enter** twice to confirm.
1. When the *Network adapter settings* screen refreshes, you should see the new name. If not, repeat Steps 4-6 again, or ask for help from your professor.
1. Now, select Option 1 (*Set network adapter address*).
1. Select **S** for *Static IP address*.
1. Enter your new IP address for this machine. It will take the following form: **10.0.*UID*.2**

    > *UID* is a placeholder. In Blackboard in Grades, there is a UID column. Each student has been assigned a unique ID number for this course. You will use that number in the address above.
    >
    > For example, if my UID on Blackboard is *40*, then my address in the step above is **10.0.40.2**. (Yours will be different!)
1. In the *Enter subnet mask* field, stick with the default by keeping the field blank and hitting **Enter**.
1. In the *Enter default gateway* field, use: **10.0.*UID*.1**
1. Hit **Enter** once the configuration has complete.
1. Back in the **Network adapter settings* screen, confirm your changes from above. You should see them all displayed. If not, repeat the missing steps or as your professor for help.
1. If everything looks good, hit **Enter** to go back to the main menu screen.
1. Go back into *Network settings* and change the other network adapter's name to: **External Network**
1. Make no other changes to this adapter.
1. You're done!

## Investigation 5: VM3 Installation - Windows 11 Client

* Name: **client-cjohnson30**
* RAM: **4 GB**
* CPU: **2 processors**
* Storage: **64 GB**

### Part 1: Setup Instructions

1. In the main window, you should see a large + symbol icon titled **Create a New Virtual Machine**. Click it.
1. In the new dialog box, keep *Typical* selected and click the **Next** button.
1. On the next screen, *Guest Operating System Installation*, do the following:
   1. Select *Installer disc image file (ISO):*
   1. Now click **Browse**.
      1. Navigate to where you saved your ***Windows 11 Education*** downloaded ISO and select it.
   1. Once selected, the previous screen should now say *"Windows 11 x64 detected."* If it doesn't, you haven't selected the right file, or your download was corrupted. Ask for help.
   1. Click **Next**.
1. On the "Name the Virtual Machine" screen, do the following:
   1. Virtual machine name: client1-*senecausername*

      > For example, if my Seneca e-mail address is `cjohnson30@myseneca.ca`, then my Seneca username is *cjohnson30*. This would give me a VM name of *client1-cjohnson30*.

   1. Location: If using an external SSD (like with our lab computers), click **Browse** and navigate to your external SSD.
      1. Create the following directory structure in your SSD: OSM620 > Virtual Machines
      1. Select this new Virtual Machines folder.
      1. Make sure you now see this change in the Location field. (Example: Z:/OSM620/Virtual Machines)
   1. Click **Next**.
1. On the "Encryption Information" screen, do the following:
   1. Select *Only the files needed to support TPM are encrypted.*
   1. Enter the same password as your other VMs in both fields.
   1. **Uncheck** the *Remember the password on this machine in Credentials Manager* option.
   1. Click **Next**.
1. On the "Specify Disk Capacity" screen, do the following:
   1. Maximum disk size (GB): **64**
   1. Select *Split virtual disk into multiple files*.
   1. Click **Next**.
1. On the "Ready to Create Virtual Machine" screen, do the following:
   1. Click on **Customize hardware...**
1. On the new "Hardware" screen, do the following:
   1. Select *Memory*, and change the value to: **4096**
   1. Select *Processors*, and change:
      1. Number of processors: **2**
      1. Number of cores per processor: **1**
      1. Virtualize Intel VT-x/EPT or AMD-V/RVI: **Checked**
      1. Virtualize CPU performance counters: ***Unchecked***
      1. Virtualize IOMMU (IO memory management unit): **Checked**
   1. Select *Network Adapter* and confirm:
        1. *Connected at power on:* **Checked**
        1. *NAT*: **Checked**
   1. Click on the ***Add...*** button on the bottom left of the *Hardware* window.
        1. Select *Network Adapter* and click **Finish**.
        1. Back in the *Hardware* window, click on *Network Adapter 2*.
        1. Under *Network connection*, click the **Custom: Specific virtual network** radio button.
        1. Just below that, click the drop-down (it likely says *VMnet0* by default). Find and select **VMnet10**.
        1. Click **Close**.
1. Back in the "Ready to Create Virtual Machine" screen, click **Finish**.
1. The virtual machine should launch.
1. If you get a dialog box about *Side channel mitigations*, check the box for *Do not show this hint again* and click **OK**.
1. Your new Virtual Machine should now finish creating and then turn on and begin the OS installation.
1. Windows installation is automated at this point and won't require any input from you. It may restart several times.

    > **Time Note:** Installation may take some time.
    >
    > Feel free to get some caffeine or make a sandwich.

1. Eventually, you will be presented with the desktop and the VMware Tools installer having completed and asking if you'd like to restart. Choose **Yes**.
1. Once you've restarted, you're installation is complete.

### Part 2:  Installation Options

1. Once the Windows 11 Setup screen appears:
1. On *Select language settings*, keep the defaults and click **Next**.
1. On *Select keyboard settings*, keep the defaults and click **Next**.
1. On *Select setup option*, do the following:
    1. Select *Install Windows 11*
    1. Check the box next to *I agree everything will be deleted, including files, apps, and settings*
    1. Click **Next**.
1. On the *Product key* page, enter your product key and click **Next**.
1. On *Applicable notices and license terms*, click **Accept**.
1. On *Select location to install Windows 11*, keep the defaults and click **Next**.
1. On *Ready to install*, click **Install**.
1. The Windows Installer will now install the OS. This may take some time, and the percentage may freeze at certain points. Be patient.
1. When the installer finishes, Windows 11 will start up and you will be launched into the First-Run Setup. Go to Part 3.

### Part 3:  First-Run Setup

1. On *Is this the right country or region?*, select **Canada** and click **Yes.**
1. On *Is this the right keyboard layout or input method?*, stick with the default and click **Yes**.
1. On *Want to add a secondary keyboard layout?*, click **Skip**.

Windows will now check for available updates from the Internet. If it finds any, it will install them automatically.

This process may take some time. Please be patient. Your VM may restart on its own.

### Part 4: Account Creation

Now that language/keyboard and installer updates have been applied, it's time to create your account.

1. On *Let's set things up for work or school*, select **Sign-in options**.
1. On this next screen, click on **Domain join instead**.
1. On *Who's going to use this device?*, enter your **Seneca username**, (*Not* your full name), then click **Next**.
1. On *Create a super memorable password*, enter the same password you've used for your other VMs and click **Next**.
1. Confirm it on the next screen and continue.
1. On *Now add security questions*, fill out three security questions, clicking **Next** after each.
1. On *Let Microsoft and apps use your location*, select **No**, then click **Accept**.
1. On *Find my device*, select **No**, then click **Accept**.
1. On *Send diagnostic data to Microsoft*, scroll down to select **Required only**, then click **Accept**.
1. On *Improve inking & typing*, select **No**, then click **Accept**.
1. On *Get tailored experiences with diagnostic data*, select **No**, then click **Accept**.

Windows will now check for *more* available updates. As before, if it finds any, it will install them automatically.

This process may take some time. Please be patient. Your VM may restart on its own.

Once complete, you will be presented with a login screen. Move to the next part to continue.

## Investigation 6: Post-Installation Tasks - Windows 11

In this investigation, we'll log in for the first time and run through several post-installation tasks both necessary and for user comfort.

### Part 1: First Login

1. Enter your password to login. First-login may take a few minutes as your profile is set up.

### Part 2: Installing VMware Tools

1. Once presented with the desktop, the very first thing we'll do is install the **VMware Tools** to integrate better with the application.
1. Outside of the VM window, way at the top of the actual VMware Workstation application, look for the **VM** menu item. (The order at the top is *File*, *Edit*, *View*, *VM*, *Tabs*, *Help*, if you're having trouble finding it.)
1. Click the following: **VM** > **Install VMware Tools**
1. Ignore the "AutoPlay" dialog box that pops up. It can take a while and disappears quickly.
1. Instead, open the **Start Menu**, and click on **File Explorer**.
1. In the new File Explorer window, look to the left-side menu bar.
1. Scroll down to *DVD Drive* and click it.
1. Inside *DVD Drive: VMware Tools*, find and double-click on the file: **setup64**
1. On the *User Account Control* dialog box that pops up, click **Yes**.
1. Wait for the installer to load.
1. On the first screen of the installer, click **Next**.
1. On *Choose Setup Type*, select **Complete**, then click **Next**.
1. On *Ready to install VMware Tools*, click **Install**.
1. This may take a few minutes, and the screen may flash a few times.
1. When complete, the last screen has a **Finish** button. Click it. (You have no choice!)
1. The installer will then ask you if you'd like to restart your computer. Click **Yes**.

### Part 3: Setting the Time Zone

1. Login again.
1. Find the time on the bottom right of the screen (in the VM, not your host machine!)
1. Right-click on the time and select **Adjust date and time**.
1. Check the displayed time and time zone.
1. The time should match current time, and the time zone should say *"(UTC-5:00) Eastern Time (US & Canada)"*.
1. If the time zone is wrong, change it to the value above.
1. Confirm your time zone and time matches local time.

### Part 4: Setting Internal Computer Name

When we created our VM, we gave it the name *client1-SenecaUsername*. This only applies to how VMware Workstation sees the VM, not to how the internal Windows OS sees itself. We need to change that to match.

1. In the *Settings* window you still have open (or reopen it from the Search bar), look to the left-hand menu bar and select **System**.
1. The very first thing you see at the top is the current computer name. This is what we're going to change.
1. Click on the **Rename** text link.
1. In the *Name your device* field, enter your VM's name: **client1-SenecaUsername** (replacing *SenecaUsername* with your actual username)
1. Click **Next**.
1. You will now be asked if you'd like to restart. Click **Restart now**.
1. After restarting and logging back in, go into *Settings* > *System* and confirm your computer name is now **client1-SenecaUsername**.

### Part 4: Windows Updates

A critical part of a security-conscious mindset is running regular updates. **This is NOT something you do only once at the start of installation.** You should be running these regularly to keep up to date with security fixes and zero-day exploits.

1. If you're already in the *Settings* application, look through the left menubar for **Windows Update** and click it.
1. In the *Windows Update* main screen, scroll down to **Advanced Options** and click it.
1. The very first option is *Receive updates to other Microsoft products*. Toggle this from **Off** to **On**.
1. At the top of the screen, where it says *Windows Update > Advanced Options*, click **Windows Update** to go back to the previous screen.
1. You will likely already see updates ready. Click on **Download & install all**.
1. As you might expect, this can take a while. Timing will depend on your Internet connection, how fast your computer is, how fast your SSD is, and how many updates there are. Please be patient. Your computer may restart.
1. Once updates have begun, take a break while it does its thing. Grab a drink, make a sandwich, text a friend.
1. After updates are complete, go back into *Windows Update* and click **Check for updates** again. There may be (and often times are) more.
1. If there are more updates, complete Steps 5-8 again until there are no more updates available.
1. In *Windows Update*, scroll back down to **Advanced options** again and click it.
1. Inside *Windows Update > Advanced options* scroll down to **Optional updates** and click it.
1. Select all available updates that appear (you may have to expand some lists).
1. Click **Download & install**.

* Windows Activation
* Theme Changes (Dark Mode)
* Internet Connectivity Check w/IE
* Install Firefox and Make Default
* Slim Down Firefox and Change Search
* Remove Copilot
