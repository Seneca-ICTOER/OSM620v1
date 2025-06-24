---
id: lab4
title: Lab 4 - Implementing DHCP
sidebar_position: 4
description: Lab 4 - Implementing DHCP
---

# Lab 4 - Implementing DHCP

## Investigation 1: Disabling VMware's NAT DHCP

When you first created your three VMs, you selected the built-in VMware NAT network. Along with providing Internet connectivity, it also provides a DHCP server to automatically assign each virtual machine its network information.

We are going to be rolling our own DHCP server on *srv1*. This means we have to **disable** the DHCP server in VMware Workstation. Otherwise, we'll have two DHCP servers by the end of this lab, causing all kinds of conflicts.

Your *srv2* and *client1* VMs will temporarily lose IP information until we complete this lab, but since we set *srv1* to static network configuration in Lab 3, it won't be affected!

Let's disable the VMware DHCP server.

### Part 1: Disable VMware DHCP

1. Open **Virtual Network Editor** in VMware Workstation (needs to be run as Administrator).
2.  Find your NAT network (usually VMnet8).
3. Uncheck or clear the DHCP option for this network.
4. Save/apply your changes.
5. You may need to restart your VMs or even the VMware NAT service for the change to take effect.

## Investigation 2: Installing the DHCP Server Role on *srv1*

### Part 1: Add the DHCP Server Role

1. **Login to srv1** with your Administrator account.
2. Open **Server Manager**.
3. In the left menu, click on **Local Server** if you’re not already there.
4. At the top right, click **Manage > Add Roles and Features**.
5. In the **Add Roles and Features Wizard**:
    1. On _Installation Type_, choose **Role-based or feature-based installation**. Click **Next**.
    2. On _Server Selection_, confirm **Select a server from the server pool** and choose **srv1**. Click **Next**.
    3. On _Server Roles_, scroll down and check **DHCP Server**.
    4. If prompted, click **Add Features**.
    5. Click **Next** through _Features_ and _DHCP Server_ pages.
    6. On _Confirmation_, click **Install**.
    7. Wait for installation to finish (may take a few minutes).
    8. When you see _Installation succeeded on srv1_, click **Close**.
### Part 2: Post-Install Configuration

1. In **Server Manager**, at the top, a yellow exclamation (!) triangle will appear. Click it, then click **Complete DHCP configuration**.
2. In the **DHCP Post-Install Configuration Wizard**:
    1. Click **Commit**.
    2. Click **Close**.
## Investigation 3: Configuring DHCP on srv1

### Part 1: Create a New IPv4 Scope

1. In **Server Manager**, at the top right, click **Tools > DHCP**.
2. In **DHCP**, expand your server’s name (srv1) under **IPv4**.
3. Right-click **IPv4** and choose **New Scope…**
4. In the **New Scope Wizard**:
    1. Click **Next**.
    2. For _Scope Name_, enter: **OSM620 Lab Scope**
    3. Click **Next**.
    4. For _IP Address Range_:
	    1. **Start IP address:** 192.168.245.100
	    2. **End IP address:** 192.168.245.199
	    3. **Subnet mask:** 255.255.255.0
	    4. Click **Next**.
	5. For _Add Exclusions_, leave blank. Click **Next**.
    6. For _Lease Duration_, leave default (8 days). Click **Next**.
    7. For _Configure DHCP Options_, select **Yes, I want to configure these options now**. Click **Next**.
### Part 2: Configure DHCP Options

1. **Router (Default Gateway):**
	1. Enter your gateway IP from Lab 3, click **Add**, then **Next**.
		1. You can also check it now by opening Command Prompt and running: `ipconfig`
2. **Domain Name and DNS Servers:**
	1. For _Parent domain_, enter your DNS domain (e.g., cjohnson30.com).
	2. For _DNS Servers_, your earlier DNS IP addresses should already be present.
	3. Click **Next**.
3. **WINS Servers:**
	1. Leave blank. Click **Next**.
4. **Activate Scope:**
	1. Select **Yes, I want to activate this scope now**. Click **Next**.
	2. Click **Finish**.
### Part 3: Confirm DHCP Scope and Settings

1. In the DHCP console, expand **IPv4 > OSM620 Lab Scope > Address Pool**.
2. Make sure the address range is correct (should be .100 to .199).
3. Under **Address Leases**, you won’t see anything yet—leases will appear as clients connect.

### Part 4: Setting DHCP Reservations

Any servers on our network should have unchanging IP addresses so they can always be found. We did this manually with *srv1*, but we can use **Reservations** to give our other machines specific IP addresses.

When one of our VMs first boots up, it will go through the four-way DHCP handshake with the DHCP server to get networking information. By default, the DHCP server on *srv1* will assign a randomly chosen, currently-unused IP address from our address pool (.100 to .199).

An IP reservation will cause the DHCP server to, instead, *always* give a specific machine the exact IP address we tell it to, and never give it out to others.

Normally, you'd only do this for other servers on your network and let basic clients receive a random address, but we'll reserve addresses for both *srv2* and *client1* for proof-of-concept.

1. On *srv2*, run `ipconfig /all` and write down the value on the *Physical Address* line. We'll need this shortly.
2. Do the same thing on *client1*.
3. Back on *srv1*, right-click on the *Reservations* folder and select **New Reservation**.
4. For *srv2*:
	1. Reservation name: **srv2-senecaUsername** (Ex: srv2-cjohnson30)
	2. IP address: **192.168.245.102**
	3. MAC address: **00-0C-29-7F-45-47**
	4. Description: **Windows Server 2025 Datacenter Core**
	5. Supported types: **Both**
	6. Click **Add**.
	7. Verify your new reservation is there by looking inside the *Reservations* folder.
5. For client1:
	1. Reservation name: **client1-senecaUsername** (Ex: client1-cjohnson30)
	2. IP address: **192.168.245.103**
	3. MAC address: **00-0C-29-88-7E-73**
	4. Description: **Windows 11 Education Client**
	5. Supported types: **Both**
	6. Click **Add**.
	7. Verify your new reservation is there by looking inside the *Reservations* folder.
## Investigation 4: Switching Clients to Use the New DHCP Server for DNS

Your _srv2_ (Server Core) and _client1_ (Windows 11) VMs are already set to receive their IP address via DHCP, but you previously set their DNS settings to point directly at _srv1_ during Lab 3. Now that _srv1_ is a fully working DHCP server, you’ll need to reset both VMs’ DNS settings to automatic so they get both their IP and DNS server from _srv1_.

### Part 1: Set srv2 (Server Core) DNS to DHCP

1. Log in as Administrator.
2. At the prompt, run:

```powershell
Get-NetIPInterface
```

3. Note the **InterfaceIndex** for your network adapter. (Likely 4, but check!)
4. Set the DNS server to automatic (DHCP):

```powershell
Set-DnsClientServerAddress -InterfaceIndex 4 -ResetServerAddresses
```

5. To apply changes, renew your DHCP lease:

```powershell
ipconfig /release
ipconfig /renew
```

6. Verify that the new DNS server is set by running:

```powershell
Get-DnsClientServerAddress
```

7. You should see the _srv1_ IP address listed as the DNS server.

### Part 2: Set *client1* (Windows 11) DNS to DHCP

1. Login as Administrator.
2. Right-click the **Network** icon in the system tray, click **Network and Internet settings**.
3. Click **Ethernet**.
4. Scroll down to *DNS server assignment* and click the **Edit** button next to it.
5. In the *Edit DNS settings* pop-up window, click the drop-down menu to change it from *Manual* to **Automatic (DHCP)**.
6. Leave all others on their defaults and click **Save**.
7. Open Command Prompt and run:

```ms-dos
ipconfig /release
ipconfig /renew
```

8. Verify your IP settings, including DNS:

```ms-dos
ipconfig /all
```

9. You should see your new IP address along with the same DNS address as before, but all supplied through DHCP.

## Investigation 5: Testing DHCP Functionality

### Part 1: Check Leases in DHCP Manager

1. On _srv1_, open **DHCP Manager**.
2. Expand **IPv4 > OSM620 Lab Scope > Address Leases**.
3. Confirm you see entries for _srv2_ and _client1_ with their assigned IPs.
### Part 2: Test DHCP & DNS Functionality

1. On both _srv2_ and _client1_, run:

```powershell
ipconfig
```

2. Confirm both the **IPv4 address** and **DNS server** match your DHCP scope and _srv1_’s IP address.
3. Try resolving and pinging your servers:

```powershell
nslookup srv1.cjohnson30.com
nslookup eff.org
ping srv1.cjohnson30.com
```

4. If everything works, you’re done! (If it doesn’t, double-check your steps or ask for help.)
