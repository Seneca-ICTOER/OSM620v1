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

 1. Open the Server Manager application.
 2. Click Manage in the top-right, then click Add Roles and Features.
 3. In the Before you begin screen, click Next.
 4. Installation Type: Keep Role-based or feature-based installation selected and click Next.
 5. Server Selection: Ensure your local server (srv1) is selected. Click Next.
 6. Server Roles: Check Hyper-V.
    1. When prompted to Add features that are required for Hyper-V, click Add Features.
    2. Click Next.
 7. Features: Leave defaults (the Hyper-V Management Tools are already included). Click Next.
 8. Hyper-V page:
    1. When asked about Virtual Switches, do not select any adapters here. We will create and name the switch manually in the next part. Click Next.
    2. Migration for live migrations: leave unchecked. Click Next.
    3. Default Stores: leave defaults. Click Next.
 9. Confirmation: Check Restart the destination server automatically if required. Click Install.
 10. Wait for installation to complete. If prompted, allow the reboot. Log back in when finished.

> **Note:** It’s normal for Server Manager to take a minute or two after reboot to show the Hyper-V tile.

### Part 2: Create the Hyper-V Virtual Switch

You will create an External Hyper-V switch bound to your Internal Network adapter (the VMware VMnet10 NIC you configured earlier).

The switch name must be: Internal Network (Hyper-V).

 1. In Server Manager, click Tools (top-right) and select Hyper-V Manager.
 2. In the left pane, click your server name (e.g., srv1-…).
 3. In the right Actions pane, click Virtual Switch Manager….
 4. Under Create virtual switch, select External, then click Create Virtual Switch.
 5. In the Virtual Switch Properties window:
    1. Name: Enter Internal Network (Hyper-V).
    2. External network: From the drop-down, select your Internal Network adapter.

        > **Reminder:** This is the adapter you renamed earlier to Internal Network and set to 10.0.`UID`.1/24. Do not choose the NAT adapter.

    3. Ensure Allow management operating system to share this network adapter is checked.
    4. Click OK. If you see a warning about temporary network disruption, click Yes.
    6. Wait for the switch to be created. This may briefly interrupt connectivity on that adapter.

> **Naming note:** You are creating an External Hyper-V switch, but you’re binding it to the Windows NIC you named Internal Network.
>
> That’s correct.
>
> The switch itself is external (bridged to that NIC), and the required name for the switch is Internal Network (Hyper-V).

### Part 3: Confirm IP Configuration (post-switch)

When you create an External switch, Windows moves IP settings from the physical adapter to a new host vNIC named vEthernet (Internal Network (Hyper-V)).

 1. Open Control Panel > Network and Internet > Network and Sharing Center > Change adapter settings.
 2. Verify you now see vEthernet (Internal Network (Hyper-V)).
 3. Right-click it → Status → Details… and confirm:
    * IPv4 Address: **10.0.`UID`.1**
    * Subnet Mask: **255.255.255.0**
 4. If the IP didn’t carry over, set it manually on vEthernet (Internal Network (Hyper-V)) to: **10.0.`UID`.1/24**
 5. Leave Default gateway and DNS for this adapter as you specified earlier in Lab 1.

### Part 4: Attach VMs (when you create them)

When you begin creating Hyper-V VMs on srv1, select Internal Network (Hyper-V) for the VM’s Network Adapter.

Do not select the “Internal” switch type here—your switch is an External Hyper-V switch bound to the Internal Network NIC, and its exact name is Internal Network (Hyper-V).

Hyper-V is now installed on srv1, and your VMs can now use the Internal Network (Hyper-V) for the lab subnet.

## Investigation 2: RRAS and NAT

## Investigation 3: Installing Windows Client 1 *(client1)*

## Investigation 4: Post-Installation Tasks *(client1*)

## Investigation 5: Cloning client1 to Create client2
