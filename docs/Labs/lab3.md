---
id: lab3
title: Lab 3
sidebar_position: 3
description: Lab 3 - Implementing DNS
---

# Lab 3 - Implementing DNS

## Investigation 1: Configuring DNS on Windows Server (*srv1*)

### Part 1: Setting a Static IP Address on *srv1*

As *srv1* will be our primary network services provider, we have to give it a **static IP address**. This is so it doesn't periodically change; if this were to occur, any other machines relying on this one would suddenly be unable to connect and lose access to all services provided, including the very DNS we're about to set up!

**Note: You will be changing network information. It is best to do *Part 1* directly on the machine, not through a remote connection.**

To set this server with an static IP address:
1. Open Command Prompt and run the following: `ipconfig /all`
2. Write down the current address information *srv1* has:
	1. IPv4 address: 10.88.111.14
	2. Subnet Mask: 255.255.255.0
	3. Default Gateway: 10.88.111.254
	4. DNS Servers: 66.207.192.6, 206.223.173.7
3. In *Server Manager* > *Local Server*, in the *Properties* area of the page, find the line entry: **Ethernet0**
4. Click the link next to it: **IPv4 address assigned by DHCP, IPv6 enabled**
5. This will open the *Network Connections* window.
6. Right-click on *Ethernet0* and select **Properties** from the drop-down menu.
7. In the new *Ethernet0 Properties* window, click on the line item (**not the checkbox**) for **Internet Protocol Version 4 (TCP/IPv4)**.
8. Further down on the same window, find and click on the **Properties** button.
9. In the new pop-up window *Internet Protocol Version 4 (TCP/IPv4) Properties*, in the *General* tab, select the **Use the following IP address:** option.
10. Enter the following information in the fields below from your previously-written *srv1* address information:
	1. IP address
	2. Subnet mask
	3. Default gateway
11. Select the **Use the following DNS server addresses:** option.
12. Enter the following information in the fields below from your previously-written *srv1* address information:
	1. Preferred DNS server: **127.0.0.1** (< This is important!)
	2. Alternate DNS server: Choose one from your written records, it doesn't matter which.
13. Click **OK**.
14. Back in the *Ethernet0 Properties* window, click **Close**.
15. Open *Firefox* and go to **eff.org** to confirm you haven't lost Internet connectivity. If you can't access the page, go back through these steps or ask for help. Do not continue forward until this works!
16. Close the *Network Connections* window.
17. Verify your change in *Server Manager > Local Server*. The earlier line entry should now simply say your IP address instead of "assigned by DHCP".

### Part 2: Installing the DNS Server Role on *srv1*

1. **Login to srv1** with your Administrator account.
2. Open the **Server Manager** application (icon is on the taskbar or Start menu).
3. In the left menu, click on **Local Server** if you’re not already there.
4. At the top right, click **Manage > Add Roles and Features**.
5. In the **Add Roles and Features Wizard** window:
    1. On _Installation Type_, select **Role-based or feature-based installation**, then **Next**.
    2. On _Server Selection_, confirm **Select a server from the server pool** and choose **srv1**, then **Next**.
    3. On _Server Roles_, scroll down and check the box for **DNS Server**.
    4. A pop-up will ask to add required features, click **Add Features**.
    5. Back on the _Server Roles_ page, click **Next**.
    6. On the _Features_ page, leave defaults, click **Next**.
    7. On the _DNS Server_ page, read and click **Next**.
    8. On the _Confirmation_ page, click **Install**.
    9. Wait for installation to finish (may take a few minutes).
    10. When you see _Installation succeeded on srv1_, click **Close**.
### Part 3: Configuring a New DNS Zone

1. Back in **Server Manager**, in the top right, click **Tools > DNS** to open the DNS Manager.
2. In the left pane, expand **srv1** and then **Forward Lookup Zones**.
3. Right-click on **Forward Lookup Zones** and select **New Zone…**
4. In the **New Zone Wizard**:
    1. On _Zone Type_, select **Primary zone**, click **Next**.
    2. On _Zone Name_, enter ***yourSenecaUsername*.com**, replacing *yourSenecaUsername* with your actual username.
	    1. For example, mine might be: **cjohnson30.com**
    3. Click **Next**.
    4. On _Zone File_, keep **Create a new file** selected, click **Next**.
    5. On _Dynamic Update_, keep **Do not allow dynamic updates** (default), then click **Next**.
    6. Click **Finish** to create the zone.

### Part 4: Adding Host (A) Records

1. In **DNS Manager**, expand your new **yourSenecaUsername.com** zone.
2. Right-click in the right pane and select **New Host (A or AAAA)…**
3. For each of your lab VMs, create a record:
	1. **srv1**
        - Name: srv1
        - IP address: (Use the IPv4 address of srv1 from ipconfig)
        - Click **Add Host**
	2. **srv2**
        - Name: srv2
        - IP address: (Use the IPv4 address of srv2 from ipconfig)
        - Click **Add Host**
	3. **client1**
        - Name: client1
        - IP address: (Use the IPv4 address of client1 from ipconfig)
        - Click **Add Host**
4. When finished, you should see all three names listed in the zone.

### Part 5: Configure DNS Forwarders on *srv1*

We want *srv1* to handle all DNS queries for our other machines, including locations on the Internet. To do this, we have to tell *this* server where to look it if doesn't have the answer locally. If it can't answer locally, it will forward the request to an Internet-based DNS server.

1. In **DNS Manager** on srv1, right-click on your server’s name in the left pane.
2. Select **Properties**.
3. Go to the **Forwarders** tab.
4. Click **Edit…**
5. In the *IP address* field, enter the IP address from your earlier list, then hit **Enter** for it to verified. If it can reach it, you should see a domain name populate next to the IP address.
6. Add a second DNS for fallback, using Google's DNS: **8.8.8.8**
7. Make sure Google's DNS is the **second** entry in the list.
8. Click **OK** to add.
9. Click **OK** again to close Properties.
### Part 6: Testing DNS Resolution and Entries Locally

Our first task is to confirm this works locally by telling the server to talk to itself first for DNS resolution. This lets us test our DNS service and records while removing the network and firewall pieces.

1. Open **Command Prompt**.
2. To test DNS resolution functionality, run the following commands one at a time:

```powershell
nslookup srv1.cjohnson30.com
nslookup srv2.cjohnson30.com
nslookup client1.cjohnson30.com
nslookup eff.org
```

7. If each returns the proper IP address value, you're done! If not, revisit your earlier configuration steps and check to see what might be missing.
8. Don't be afraid to ask for help!

## Investigation 2: Configuring Machines For DNS Use

### Part 1: Windows Server Core (srv2)

1. Log in as Administrator.
2. At the prompt, run:

```powershell
Get-NetIPAddress
```

3. Look for the section that contains *srv2*'s normal IP address. Make a note of the **InterfaceIndex** number just below it. (For example, 4. Yours may differ.)
4. Set the DNS server to srv1’s IP (replace X.X.X.X with srv1’s actual address, and 4 with your NIC’s ifIndex):

```powershell
Set-DnsClientServerAddress -InterfaceIndex 4 -ServerAddresses 192.168.1.14
```

5. Confirm the change:

```powershell
Get-DnsClientServerAddress
```

6. To test DNS resolution functionality, run the following commands one at a time:

```powershell
nslookup srv1.cjohnson30.com
nslookup srv2.cjohnson30.com
nslookup client1.cjohnson30.com
nslookup eff.org
```

7. If each returns the proper IP address value, you're done! If not, revisit your earlier configuration steps and check to see what might be missing.
8. Don't be afraid to ask for help!
9. Last, ping each other machine to prove you no longer need to remember IP addresses:

```ms-dos
ping srv1.cjohnson30.com
ping client1.cjohnson30.com
```

13. Cool, right?

### Part 3: Windows 11 Client (client1)

1. Login as Administrator.
2. Right-click the **Network** icon in the system tray, click **Network and Internet settings**.
3. Click **Ethernet**.
4. Scroll down to *DNS server assignment* and click the **Edit** button next to it.
5. In the *Edit DNS settings* pop-up window, click the drop-down menu to change it from *Automatic (DHCP)* to **Manual**.
6. Find the new *IPv4* option and toggle it **On**.
7. In the *Preferred DNS* field, enter the *srv1* IP address.
8. Leave all others on their defaults and click **Save**.
9. Open Command Prompt and type:

```ms-dos
ipconfig /flushdns
```

 9. To test DNS resolution functionality, run the following commands one at a time:

```ms-dos
nslookup srv1.cjohnson30.com
nslookup srv2.cjohnson30.com
nslookup client1.cjohnson30.com
nslookup eff.org
```

10. If each returns the proper IP address value, you're done! If not, revisit your earlier configuration steps and check to see what might be missing.
11. Don't be afraid to ask for help!
12. Last, ping each server to prove you no longer need to remember IP addresses:

```ms-dos
ping srv1.cjohnson30.com
ping srv2.cjohnson30.com
```

13. Cool, right?

## Investigation 3: Configuring Reverse Lookup (PTR) Records

### Part 1: Create a Reverse Lookup Zone

1. In **DNS Manager** on *srv1*, right-click **Reverse Lookup Zones** in the left pane.
2. Click **New Zone…**
3. In the **New Zone Wizard**:
    1. On _Zone Type_, select **Primary zone**. Click **Next**.
    2. On _Reverse Lookup Zone Name_, choose **IPv4 Reverse Lookup Zone**. Click **Next**.
    3. On _Network ID_, enter the first three octets of your VMs’ subnet (for example, if your VMs’ IPs are 192.168.131.x, enter 192.168.131). Click **Next**.
    4. On _Zone File_, keep defaults. Click **Next**.
    5. On _Dynamic Update_, keep defaults (Do not allow dynamic updates). Click **Next**.
    6. Click **Finish** to create the zone.

### Part 2: Add PTR Records for Each VM

1. We're going to automatically add PTR records using our existing A records for ease of use.
2. Inside the *Forward Lookup Zones*, in the **cjohnson30.com** zone, right-click each A record you created (srv1, srv2, client1) and select **Properties**.
3. Check the box next to **“Update associated pointer (PTR) record”** and click **OK**.
4. If the box was already checked, uncheck it, click **Apply**, check it again, then click **Apply** again. This forces the PTR generation.
5. This should automatically create PTR records in your new reverse zone.
6. Double-check your work. Click on the folder inside *Reverse Lookup Zone* to see its contents. If empty, right-click on the folder and click *Refresh*.
7. They should now appear. If they do not, retrace your steps of ask for help.

### Part 3: Test Reverse DNS Resolution

1. On *srv2*, open PowerShell.
2. Run **nslookup** on each VM's IP address:

```powershell
nslookup 192.168.1.14
nslookup 192.168.1.15
nslookup 192.168.1.16
```

3. You should see the PTR record and corresponding hostname for each IP address. 

Output
```powershell
Server:  srv1.cjohnson30.com
Address:  10.88.111.14

Name:    client1.cjohnson30.com
Address:  10.88.111.15
```

4. Notice that the server entry no longer says "UnKnown" as it did before. Now it can identify itself!

Congratulations, you've now set up basic DNS services from *srv1* to each VM in your environment!
