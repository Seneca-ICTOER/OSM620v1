---
id: lab2
title: Lab 2
sidebar_position: 2
description: Lab 2 - Security and Remote Connectivity
---

# Lab 2 - Security and Remote Connectivity

## Lab Preparation

### Purpose / Objectives of Lab 2

In this lab, you will conduct several Windows system administration tasks to secure your servers against would-be attackers and gain preliminary experience with the command line interface.

If you encounter technical issues, please contact your professor via e-mail or in your section's Microsoft Teams group.

### Minimum Requirements

Before beginning, you must have:

1. Successfully completed Lab 1.
2. Attended the Week 3 lecture
3. Read through the Week 3 slides, and have them handy as a reference for concepts.
4. Your external SSD (or personal computer) with your VMs from Lab 1.
5. Your VM login credentials.
6. Optional, but recommended: Caffeine delivery system.

## Key Concepts

### Security: From the Beginning

In the not-too-distant past, companies would focus on getting their product and systems working and relegating security as their last step, often as an afterthought. When security is only considered at the end of a project, it's very difficult to remember all the ways in which your product interacts and things can get missed.

This created several high-profile breaches in the 90s and early 2000s, and our approach to security had to be reconsidered.

As a result, we now consider security **from the beginning**. As you create applications, add users to databases, create links between services, you _must_ keep security in mind at every step of development. Securing as you go is the best method, but even something as simple as simply documenting unsecured parts of your code as you go can be enough (assuming you go back and fix them!)

Generally, we apply the concept of [Principle of Least Privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) to security. Essentially, this boils down to locking everything down as much as possible and only allowing what and who you need through. Open access makes you a target. You'll be applying this principle to the firewall later in this lab.

We also take a look at defaults. Most systems and software come with pre-configured defaults to make out-of-the-box setup easy. This can take the form of a default username and password, default ports, etc. In a well secured system, these are often changed to avoid hack attempts. If you know the default, there's a high chance that hackers know it as well. You'll be changing some defaults in this lab.

This is not an exhaustive list of applied security, but it does give use a bit of working knowledge. You'll need it for this lab as well as in our later work.

### Firewalls

In short, **a firewall is a utility that sits on your computer between your network connection and the rest of your system.**

Any application, service, or other data that is sent or received by your computer goes through your firewall first. The dominant network protocol is TCP/IP, which means we’re dealing with *packets*.

**A firewall looks at these packets.**

To be clear, the firewall doesn’t look inside packets, but just at the outside data like IP address and/or port destination, etc. The actual transmitted data is still secure and unread.

Generally with firewalls, we apply the _Principle of Least Privilege_ by dropping all new connections by default, and allowing a few exceptions. This is known as **whitelisting**.

### Editing Text Files

As you will sometimes be working in the Windows PowerShell command line environment, it is useful to learn a least one common method of editing text files.

Although programmers and developers usually use graphical IDE's to code and compile programs (Visual Studio, Sublime, Eclipse, etc), they can create source code using a text editor and compile their code directly on the server to generate executable programs (without having to transfer them for compilation or execution).

Developers very often use a text editor to modify configuration files. In this course, you will become familiar with the process of installing, configuring, and running network services. Text editors are an important tool to help this setup, but are also used to "tweak" or make periodic changes in service configurations.

The two most readily-available command line text editor built into Windows is **Notepad**.

However, Notepad is not available in Server Core. To edit a text file in that environment, we have three main options:
1. Use PowerShell's object-oriented programming to send an edit directly into a text file. This is cumbersome and is not interactive (you don't see the text file on screen), but it is the only built-in option.
2. Transferring the file to a different computer that does have a text editor (like your Windows 11 client), modifying the file there, and transferring it back to your Server Core machine.
3. Using **Visual Studio Code** to connect remotely the the environment. This is by far the coolest and most convenient option.

We'll be doing all three in this lab to show you how, but going forward, VS Code will be our go-to for interacting with Server Core in most instances. (You will be tested on all three options, so don't skip them!)

## Investigation 1: Windows Defender (Firewall)

In this investigation, we're going to take a look at the Windows Defender firewall to see how firewall rules can be applied to secure our servers and let the few things we want to allow through.

It should be noted that the Windows Defender firewall *should not be your only defense*. Production environments will often have managed networks that restrict access on a larger scale, some of which you will get into with your networking courses.

These work together, though we will only be focusing (mostly) on the Windows firewall in this course.

### Part 1: Windows Server GUI (srv1) - Configuring the IIS Role

On this server, we will configure our first server role, IIS (a web server). This will be used only for testing connectivity between your other VMs and working with the firewalls.

We will spend more time with Server Roles in a later lab. For now, simply follow the instructions.

1. In the *Server Manager* application, in the menu bar on the left side of the window, click on **Local Server**.
2. Now, at the top right of the window, click **Manage** > **Add Roles and Features**.
3. The *Add Roles and Features Wizard* dialogue box pops up.
4. On the first page, *Before you begin*, check the box next to **Skip this page by default**, then click **Next**. This allows us to skip this page any other time we want to add a role or feature in later labs.
5. On the *Installation Type* page, select **Role-based or feature-based installation** and click **Next**.
6. On the *Server Selection* page, select **Select a server from the server pool**, then **srv1-username**, and finally **Next.**
	1. Note: In later labs, we'll be able to target other servers for remotely installing features. Here, we're selecting the local server.
7. On the *Server Roles* page, this is where we'll select our IIS web server. Scroll through the listing until you find **Web Server (IIS)**, check the box next to it, and click **Next**.
8. A secondary dialogue box, *Add features that are required for Web Server (IIS)?*, pops up. Make sure the **Include management tools (if applicable)** box is checked, then click **Add Features**.
9. Back in the *Server Roles* page, click **Next** again.
10. On the *Features* page, leave all settings as their defaults and click **Next**.
11. On the *Web Server Role (IIS)* page, click **Next**.
12. On the *Role Services* page, keep all defaults and click **Next**.
13. Finally, on the *Confirmation* page, click **Install**.
14. This may take a few minutes. Please be patient.
15. When the wizard has the status message *"Installation succeeded on srv1."*, setup is complete and you can click **Close**.
16. Verify your local web server works by opening *Firefox* and going to the following address: **127.0.0.1**
17. If you see the **Internet Information Services** splash page, you've successfully completed the installation and can move on to the next part!

(Insert instructions for loading this page on the Windows 11 client to test connectivity.)
(Insert instructions for loading this page on Windows Server Core if possible, even just unrendered HTML code.)

### Part 2: Testing VM Network Connectivity

As part of your Lab 1 environment setup, you tested your connection to the Internet from each of your 3 virtual machines.

It's now time to test if we can use each VM to connect to the others.

1. On your Windows Server GUI (srv1) VM, open Command Prompt.
2. Grab this VM's IP address with the following command and write it down: `ipconfig`
3. On your Windows Client (client 1) VM, open Command Prompt.
4. Enter the following command to test our ability to talk to srv1: `ping "srv1-ipaddress"` where *srv1-ipaddress* is the IP address from Step 2.
	1. Example: `ping 192.168.1.14`
5. It doesn't work, does it? That's normal at this stage and we'll fix it below. For now, we'll try connecting to our web server on srv1. That should show us the two VMs can talk to each other.
6. Open *Firefox* on your **Windows 11 Client (client1)** and use the IP address from Step 2 (your srv1 IP address) as the URL.
	1. Example: `http://192.168.1.14`
7. Can you see the IIS splash page that you saw in Part 1, Step 17? If so, you have connectivity!
8. Continue to Part 3.

### Part 3: Windows Server GUI (srv1) - Applying Firewall Rules

We will now apply our security-conscious policy by configuring our firewall on this server.

At the moment, the server's firewall is configured using defaults. As mentioned above, defaults are a security risk as they are known to everyone and can be used against you. If an attacker *doesn't* know your configuration, it's harder for them to know what's open and what's not and how to attack.

As you saw from Part 2, ping between client1 and srv1 didn't work. This is because, by default, the ability to ping a server is turned off. A ping (a type of ICMP packet) is typically used to see if you can get a response from a server. Having a server respond let's an attacker know there's a machine there that they can then try to break into.

We want to turn on ping so we can test connections between our machines, but we have to be careful. Turning that on through the firewall too broadly opens us up to that vulnerability.

We are going to turn it on *only* for our local network. Our VMs will be allowed to ping each other, but anything outside of our subnet (192.168.1.0/24) can't. Best of both worlds.

To do this, we're going to work with the **Windows Defender Firewall** on srv1.

1. In the *Server Manager* application, go to *Local Server*.
2. In the *Properties* section of this page, look for the **Microsoft Defender Firewall** line item.
3. Next to the line, it should say **Public: On**. Click on this.
4. The *Windows Security > Firewall & Network protection* application opens.
5. On this screen, you will see three networks: *Domain network*, *Private network*, and *Public network*.
6. We'll spend more time with these in later weeks, but for now, all three should say: **Firewall is on**.
7. Below this, click on the link that says: **Advanced settings**
8. This opens the *Windows Defender Firewall with Advanced Security* application.
9. On the first page, you'll notice the same three profiles: *Domain Profile*, *Private Profile*, and *Public Profile*.
10. All three have the same overall rules:
	1. **Windows Defender Firewall is on**: This just confirms the firewall is active for this network profile.
	2. **Inbound connections that do not match a rule are blocked**: This means that all incoming connections and requests (like trying to ping this machine) are blocked *by default*. If you want to allow a certain type of connection or service into your server, you have to make a specific rule for it. This is whitelisting and our *Principle of Least Priviledge* in action.
	3. **Outbound connections that do not match a rule are allowed**: This means all network data leaving the server is automatically allowed. The logic here is that if the server is the one deciding the send out information, it's likely fine. (Note: The only time we ever whitelist outbound connections is for specialized security settings like government compliance.)
11. At the moment, we're dealing with the *Public Profile* context. Let's allow ICMP ping!
12. On the left-hand menu bar, click **Inbound Rules**.
13. This loads a ton of already-defined rules. Thankfully, the one we need has already been defined. We just need to turn it on.
14. At the top of this area, click **Name** to order the list by name (this is not the default).
15. Now, scroll down until you can find the following and double-click it: **Core Networking Diagnostics - ICMP Echo Request (ICMPv4-In)**, **Private, Public**.
	1. **Note:** There are two of these rules! Look for the one that has **Private, Public** under the Profile header. The wrong one says Domain.
16. This opens this rule's configuration window, starting on the *General* tab.
17. In the *General* tab, look for the following and check the box next to it: **Enabled**
18. Click **Apply**, then **OK**.
19. Back in the main *Inbound Rules* window, you should see that same rule line now says **Yes** under the *Enabled* header.
20. You've enabled ICMP ping! Let's go test it.
21. Switch back to your client1 machine, and run the same ping you ran earlier pointing to srv1. (Refer to *Part 2, Step 4*.)
22. Does it work?
23. It if does, congratulations! You've just enabled ping for connectivity checking and gone through your first foray into the Windows Firewall.

> ℹ️ **A note for later labs:**
> By default, this rule is set to only allow incoming pings (ICMP requests) from computers on your **VM network**—that is, other virtual machines on the same VMware NAT or host-only network as your server—not from the wider Internet or any physical computers in the classroom.
> 
> You can see this by checking the **Scope** tab in the rule’s properties, where “Remote IP address” is set to “Local subnet.”
> 
> We’ll spend more time on how **Scope** and **Private/Public profiles** affect your firewall rules in our _Secondary Network_ assignment.

> **📝 Lab Question:**
> Why did we _not_ have to do this for our IIS web server setup?
> 
> In the **Inbound Rules** list, scroll through to see if you can find the rule that’s allowing web server pages to be requested from *srv1*.
> 
> Write down the name of the rule in your Lab Logbook when you find it (it’s not called IIS) and explain why you think you didn’t have to enable this rule yourself. Think back to when you installed the Server Role.

### Part 3: Windows Server Core (srv2) - Applying Firewall Rules

(Insert instructions on firewall whitelisting, then adding a rule for ICMP ping. This will be done with PowerShell.)
(On Windows Server GUI and then Windows 11 client, test ping for success.)

### Part 4: Windows Client (client1) - No Rules

(Briefly explain why only basic firewall protection is enabled, as it's just a client machine. Should discuss the difference between Public and Private scopes.)

(Ping should be enabled, though, for future connectivity testing, but only on the local network.)

## Investigation 2: Remote Management - Windows Server GUI (srv1)

While you have direct access to all three VMs from VMware, these days most machines are remote. This means you typically do not have direct, physical access to the servers.

Even if you do, having remote access to allow you to manage your servers from the comfort of your office (or home!) instead of walking to each physical machine is far better.

In this investigation, we'll set up remote access to our Windows Server GUI (srv1) so we can connect to it using your Windows 11 Client VM.

### Part 1: Enabling Remote Desktop Connections

In this part, we'll turn on Remote Desktop (RDP) on the server.

(Insert step-by-step instructions)

### Part 2: Adding an RDP Firewall Rule

In this part, we'll add a firewall rule to allow the connection over the local network.

(insert step-by-step instructions)

### Part 3: Connecting to Windows Server (srv1) from Windows 11

In this part, we'll verify our work by connecting to the server using our Windows 11 client VM.

(Insert step-by-step instructions)

## Investigation 3: Remote Management - Windows Server Core (srv2) with Remote Desktop

In this investigation, we'll set up remote access to our Windows Server Core (srv2) so we can connect to it using your Windows 11 Client VM.

### Part 1: Enabling Remote Desktop Connections

In this part, we'll turn on Remote Desktop (RDP) on the server.

(Insert step-by-step instructions)

### Part 2: Adding an RDP Firewall Rule

In this part, we'll add a firewall rule to allow the connection over the local network.

(insert step-by-step instructions)

### Part 3: Connecting to Windows Server (srv2) from Windows 11 via RDP

In this part, we'll verify our work by connecting to the server using our Windows 11 client VM.

(Insert step-by-step instructions)

### Part 4: File system navigation

(A primer on file system navigation in Windows. Have them create a few directories and empty files using CLI only.)

### Part 5: Editing a file

(This is where we do the single example of using PowerShell to modify a text file.)

## Investigation 4: Remote Management - Windows Server Core (srv2) with SSH

### Part 1: Enabling SSH Connections

In this part, we'll turn on incoming SSH connections so we can connect to our server using Visual Studio Code from the Windows 11 client.

(Insert step-by-step instructions for enabling SSH on srv2 via PowerShell commands)

### Part 2: Adding an SSH Firewall Rule

### Part 3: Connecting to Windows Server Core (srv 2) from Windows 11 via SSH

## Investigation 5: Remote Management - Windows Server Core (srv2) with Visual Studio Code + SSH

### Part 1 : Connecting to srv2 with Visual Studio Code

(insert instructions on how to use the UI to connect, including saving the connection for future use)

### Part 2: A Quick Tour of VS Code + Remote SSH

(A brief tour of the three panes: File navigation, text editor, and PowerShell terminal)

### Part 3: VS Code for Fun and Profit

(Brief exercises having them do some file management with the navigation pane, opening and modifying a file, and then running a PowerShell command)

(Insert caveat about most **sconfig** commands not working through SSH or VS Code, they must be done through RDP because of how interaction works.)
