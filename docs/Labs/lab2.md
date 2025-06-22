---
id: lab2
title: Lab 2
sidebar_position: 2
description: TBD
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

(Insert instructions on configuring IIS.)
(Insert instructions for loading this page on the Windows 11 client to test connectivity.)
(Insert instructions for loading this page on Windows Server Core if possible, even just unrendered HTML code.)

### Part 2: Windows Server GUI (srv1) - Applying Firewall Rules

We will now apply our security-conscious policy by configuring our firewall on this server.

(Insert instructions on firewall whitelisting for incoming connections, only allowing ICMP Ping for testing with the other VMs. This will prove connectivity, but also prove that the IIS page now doesn't load, which is correct.)

(Insert instructions on adding a firewall rule for incoming HTTP for IIS, then have students try to load the page on the Windows 11 client again. If it works, then Part 2 is complete.)

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
