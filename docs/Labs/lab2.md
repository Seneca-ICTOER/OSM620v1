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

Our server now has access to two networks.

* **External Network**: Connection to the Internet
* **vEthernet (HQ Network)**: Internal network only between *srv1* and the Hyper-V VMs we'll create in Investigation 3. This network *does not* have access to the Internet.

If we want to give our Hyper-V machines Internet access, we need to route network traffic between the two networks using *srv1* as a bridge. This keeps our Hyper-V machines on a secure network, and Internet access is handled and monitored by our Windows Server.

This will involve setting up routing and network address translation (NAT).

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
1. Keep the application open on *NAT* and minimize. We'll comme back to it later.
1. That's it! Move on to the next Investigation.

## Investigation 3: Installing Windows Client 1 with Hyper-V *(client1)*

### Part 4: Attach VMs (when you create them)

When you begin creating Hyper-V VMs on srv1, select Internal Network (Hyper-V) for the VM’s Network Adapter.

Do not select the “Internal” switch type here. Your switch is an External Hyper-V switch bound to the Internal Network NIC, and its exact name is Internal Network (Hyper-V).

Hyper-V is now installed on srv1, and your VMs can now use the Internal Network (Hyper-V) for the lab subnet.

## Investigation 4: Post-Installation Tasks *(client1*)

## Investigation 5: Cloning client1 to Create client2
