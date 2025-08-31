---
id: lab2
title: Lab 2 - Hyper-V, NAT, and Windows Clients
sidebar_position: 2
description: Lab 2 - Hyper-V, NAT, and Windows Clients
--- 

# Lab 2 - Hyper-V, NAT, and Windows Clients

## Investigation 1: Hyper-V Role Installation and Switch Setup *(srv1)*

In this investigation, you will install the Hyper-V role on srv1 and create a Hyper-V virtual switch that uses your existing Internal Network adapter.

Your Hyper-V switch will be named Internal Network (Hyper-V).

### Part 1: Install the Hyper-V Role

 1. Open the **Server Manager** application and go to **Add Roles and Features**.
 1. **Installation Type:** Keep Role-based or feature-based installation selected.
 1. **Server Selection:** Ensure your local server (*srv1*) is selected.
 1. **Server Roles:** Check ***Hyper-V***.
    1. When prompted to "*Add features that are required for Hyper-V*", click **Add Features**.
 1. **Features:** Leave defaults (the *Hyper-V Management Tools* are already included).
 1. **Hyper-V page**:
    1. When asked about Virtual Switches, select **Internal Network** only.
    1. Migration for live migrations: leave unchecked.
    1. Default Stores: leave defaults.
 1. Confirmation: Check "*Restart the destination server automatically if required*".
 1. Click **Install**.
 1. Wait for installation to complete. If prompted, allow the reboot. Log back in when finished.

> **Note:** It’s normal for *Server Manager* to take a minute or two after reboot to show the Hyper-V tile.

### Part 2: Rename the Hyper-V Virtual Switch

As part of our Hyper-V role installation, we selected the *Internal Network* (Part 1, Step 6.1).

This has created a virtual switch on the server. For easy management, we'll rename it.

Our new virtual switch name will be: `HQ Network`

 1. In Server Manager, click Tools (top-right) and select Hyper-V Manager.
 1. In the left pane, click your server name (e.g., srv1-…).
 1. In the right Actions pane, click Virtual Switch Manager….
 1. Under the Virtual Switches column on the left, look for the switch that's already been created. It will likely have a name similar to: `Intel(R) 82574L Gigabit Network Connection - Virtual Switch`
 1. In the Virtual Switch Properties window:
    1. Name: Change to `HQ Network`
    1. Ensure the **External network** radio button is selected.

        > **Reminder:** This is the adapter you renamed earlier to Internal Network and set to 10.0.`UID`.1.

    1. Ensure "*Allow management operating system to share this network adapter*" is checked.
    1. Click OK. If you see a warning about temporary network disruption, click Yes.

    > **Naming note:** You are creating an External Hyper-V switch, but you’re binding it to the Windows NIC you named Internal Network.
    >
    > That’s correct.
    >
    > You will end up with a third network adapter called: `vEthernet (HQ Network)`

 1. Go back to *Server Manager > Local Server* and refresh. You should now see the following two networks:
    * **External Network**: Assigned by DHCP
    * **vEthernet (HQ Network)**: IPv4 addess assigned by DHCP, IPv6 enabled

### Part 3: Configure Network Setting for Hyper-V Switch

Now that we've created the Hyper-V network adapter, we have to give it an IP address. This will let our Hyper-V VMs talk to the server, and eventually, bridge our Internet connection.

 1. In *Server Manager > Local Server*, click on the entry next to **vEthernet (HQ Network)**. This opens the *Network Connections* window.
 1. Verify you now see a third network adapter: `vEthernet (HQ Network)`
 1. Right-click it → Properties and do the following:
    1. Internet Protocol Version 6 (TCP/IPv6): **Unchecked**
    1. Internet Protocol Version 4 (TCP/IPv4): Select and click **Properties**
        1. IPv4 Address: **10.0.`UID`.1**
        1. Subnet Mask: **255.255.255.0**
        1. Leave all other fields blank and click OK.
 4. Back in *Server Manager > Local Server*, refresh. You should now see the following two networks:
     * **External Network**: Assigned by DHCP
     * **vEthernet (HQ Network)**: 10.0.`UID`.1

## Investigation 2: RRAS and NAT

Our server now has access to two networks:

* **External Network**: Connection to the Internet
* **vEthernet (HQ Network)**: Internal network only between *srv1* and the Hyper-V VMs we'll create in Investigation 3. This network *does not* have access to the Internet.

If we want to give our Hyper-V machines Internet access, we need to route network traffic between the two networks using *srv1* as a bridge. This keeps our Hyper-V machines on a secure network, and Internet access is handled and monitored by our Windows Server.

This will involve setting up routing and network address translation (NAT).

Welcome to Microsoft's **Routing and Remote Server (RRAS)**.

### Part 1: Installing the Remote Access Role

 1. Open the **Server Manager** application and go to **Add Roles and Features**.
 1. **Installation Type:** Keep Role-based or feature-based installation selected.
 1. **Server Selection:** Ensure your local server (*srv1*) is selected.
 1. **Server Roles:** Check ***Remote Access***.
 1. **Features:** Leave defaults (the *Hyper-V Management Tools* are already included).
 1. **Remote Access page:** Click Next.
     1. The **Add Roles and Features Wizard** dialog box appears. Leave defaults and select *Add Features*.
 1. **Remote Access > Role Services page:** Check the following and click *Next* when ready:
     * Direct Access and VPN (RAS)
     * Routing
 1. Keep defaults and select *Next* on the following pages:
     1. Web Server Role (IIS)
     1. Web Server Role (IIS) > Role Services
 1. Confirmation: Click **Install**.
 1. In the **Results** page: When installation has completed, click on the "*Open the Getting Started Wizard*" link.
 1. The wizard opens. Make no changes and close it. (This just removes the system nagging.)
 1. Back in **Results**, click Close.

### Part 2: Enabling NAT with RRAS

You will now install the tools for routing and NAT bridging discussed at the top of this investigation using the **Routing and Remote Access Server** (RRAS) we've just installed.

1. Open the **Server Manager** application and go to **Tools > Routing and Remote Acceess**.
1. This opens the *Routing and Remote Access* application.
1. In the right-hand column, find SRV1, right-click it, and select **Configure and Enable Routing and Remote Access**.
1. The setup wizard appears. Click *Next*.
1. **Configuration:** Select the *Custom configuration* radio button.
1. **Custom Configuration:** Select (checkbox) only the following:
    * NAT
    * LAN routing
1. **Summary window**: Click *Finish*.
1. The **Routing and Remote Access** service status dialog box appears. Click *Start service*.
1. It may take a few moments for the service to fully start. Be patient.
1. Once the *Routing and Remote Access* application reappears, move to the next part.

### Part 3: Configuring NAT with RRAS

It's now time to configure the routing and NAT bridging between the two networks.

1. Open the **Routing and Remote Access** application.
1. In the right-hand column, expand *SRV1*, then expand *IPv4*.
1. Right-click on *NAT* and select *New Interface*.
1. Select the **External Network** entry and click *OK*.
1. In the *Network Address Translation Properties* window, select the following and click OK when ready:
    * Public interface connected to the Internet
    * Enable NAT on this interface
1. Right-click on *NAT* and select *New Interface* again.
1. Select the **vEthernet (HQ Network)** entry and click OK.
1. In the *Network Address Translation Propertie*s window, select the following and click OK when ready:
    * Private interface connected to private network
1. Back in the *NAT* window, you should see two created interfaces:
    * External Network
    * vEthernet (HQ Network)
1. Keep the application open on *NAT* and minimize. We'll come back to it later.
1. That's it! Move on to the next Investigation.

## Investigation 3: Installing Windows Client 1 with Hyper-V *(client1)*

### Part 1: Creating the Hyper-V Appliance

### Part 2: Installing Windows 11 (*client1*)

* Hypervisor: **Hyper-V**
* Name: **client1-`SenecaUsername`**
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
1. Once you've restarted, your installation is complete.

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

### Part 5: Hyper-V Client Management

## Investigation 4: Post-Installation Tasks *(client1*)

In this investigation, we'll log in for the first time and run through several post-installation tasks both necessary and for user comfort.

### Part 1: First Login

1. Enter your password to login. First-login may take a few minutes as your profile is set up.

### Part 2: Setting the Time Zone

1. Login again.
1. Find the time on the bottom right of the screen (in the VM, not your host machine!)
1. Right-click on the time and select **Adjust date and time**.
1. Check the displayed time and time zone.
1. The time should match current time, and the time zone should say *"(UTC-5:00) Eastern Time (US & Canada)"*.
1. If the time zone is wrong, change it to the value above.
1. Confirm your time zone and time matches local time.

### Part 3: Setting Internal Computer Name

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

## Investigation 5: Cloning *client1* to Create *client2*

### Part 1: Exporting *client 1*

### Part 2: Renaming *client 1* to *client2*

### Part 3: Importing the New *client1*

### Part 4: Final Checks - *client1* and *client2*
