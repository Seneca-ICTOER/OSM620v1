---

id: lab5
title: Lab 5 - Implementing DHCP
sidebar_position: 5
description: Lab 5 - Implementing DHCP
---

# Lab 5 - Implementing DHCP

## Lab Preparation

### Purpose / Objectives of Lab 5

In this lab, you will deploy **DHCP** on *srv1* to automatically provide IP configuration for your internal lab network.

By the end, you will:

1. Install the **DHCP Server** role on *srv1*.
2. Create an IPv4 **scope** for your internal subnet **10.0.`UID`.0/24** with proper **options** (Router, DNS servers, DNS Suffix).
3. Create **reservations** so *srv2*, *client1*, and *client2* receive predictable addresses that match prior labs.
4. Flip *srv2*, *client1*, and *client2* from **static** addressing to **DHCP**, then verify leases.
5. Validate **DHCP + DNS** end‑to‑end with `ipconfig`, `nslookup`, and `ping`.

### Minimum Requirements

Before beginning, you must have:

* Successfully completed **Lab 4 – Implementing DNS**, with *srv1* resolving internal names and using loopback for local DNS testing.
* Your **UID** value handy.
* All four VMs present from earlier labs: *srv1* (GUI), *srv2* (Core), *client1*, *client2*.

### Key Concepts

* **DHCP** automatically assigns IP addressing (IPv4 address, subnet mask), **Default Gateway (Option 003)**, **DNS servers (Option 006)**, and **DNS Suffix (Option 015)** to clients on a subnet.
* **Scope** defines the usable address pool on a network. **Reservations** ensure specific MAC addresses always receive the same IP.
* In this course, your internal network remains **10.0.`UID`.0/24**; *srv1* is the router at **10.0.`UID`.1**.

> **Design Note:** We will keep client addresses consistent with Labs 2–4 using **reservations** so your existing DNS host records remain correct.

---

## Investigation 1: Install the DHCP Server Role on *srv1*

### Part 1: Add the DHCP Server Role

1. **Login to srv1** with your Administrator account.
2. Open **Server Manager** → **Manage > Add Roles and Features**.
3. **Installation Type**: *Role-based or feature-based installation* → **Next**.
4. **Server Selection**: choose **srv1** → **Next**.
5. **Server Roles**: check **DHCP Server** → **Add Features** if prompted → **Next** through *Features* and *DHCP Server* pages.
6. **Confirmation**: **Install** and wait for completion.

### Part 2: Post‑Install Configuration

1. In **Server Manager**, click the yellow **!** → **Complete DHCP configuration**.
2. In the wizard, click **Commit** → **Close**.

---

## Investigation 2: Create Scope and Options (10.0.`UID`.0/24)

### Part 1: Create a New IPv4 Scope

1. **Tools > DHCP**.
2. Expand your server (srv1) → **IPv4** → **Right‑click > New Scope…**
3. **Scope Name**: `OSM620 HQ`
4. **IP Address Range**:

   * **Start**: `10.0.UID.1`
   * **End**: `10.0.UID.254`
   * **Subnet mask**: `255.255.255.0`
5. **Add Exclusions and Delay**: Add the following:
    * `10.0.UID.1`
    * `10.0.UID.200` to `10.0.UID.254`
    * Leave the delay blank.
6. **Lease Duration**: default (8 days) → **Next**.
7. **Configure DHCP Options**: choose **Yes, I want to configure these options now** → **Next**.

### Part 2: Configure Scope Options

1. **Router (Default Gateway) – Option 003**: `10.0.UID.1` → **Add** → **Next**.
2. **Domain Name and DNS Servers – Option 006/015**:

   * **Parent domain** (Option 015): `yourSenecaUsername.com` *(replace with your lab domain from Lab 4)*
   * **DNS Servers** (Option 006): 
       * `10.0.UID.1` *(srv1)*
       * **149.112.121.20** *(CIRA)*
3. **WINS Servers**: leave blank → **Next**.
4. **Activate Scope**: select **Yes, I want to activate this scope now** → **Finish**.

> **Why start at `.2`?** `.1` is the gateway on *srv1*. We’ll reserve `.2`, `.11`, and `.12` for *srv2*, *client1*, and *client2* to preserve continuity with earlier labs.

---

## Investigation 3: Reservations for Predictable Addresses

We’ll bind specific IPs to each machine’s **MAC address** so they keep the same addresses used in Labs 2–4.

### Part 1: Collect MAC addresses

1. On **srv2** (Core): `ipconfig /all` → record the **Physical Address** for the **Internal** adapter.
2. On **client1**: `ipconfig /all` → record Physical Address.
3. On **client2**: `ipconfig /all` → record Physical Address.

### Part 2: Create reservations on *srv1*

In **DHCP Manager** → **IPv4 > OSM620 HQ > Reservations** → **Right‑click > New Reservation…**

Create the following (replace `UID` and MACs):

* **srv2**

  * **IP address**: `10.0.UID.2`
  * **MAC**: `<srv2 MAC>`
  * **Description**: `Windows Server 2025 Datacenter Core`
  * **Supported types**: **Both** → **Add**
* **client1**

  * **IP address**: `10.0.UID.11`
  * **MAC**: `<client1 MAC>`
  * **Description**: `Windows 11 Education`
  * **Supported types**: **Both** → **Add**
* **client2**

  * **IP address**: `10.0.UID.12`
  * **MAC**: `<client2 MAC>`
  * **Description**: `Windows 11 Education`
  * **Supported types**: **Both** → **Add**

Verify all three appear under **Reservations**.

---

## Investigation 4: Switch from Static to DHCP

### Part 1: *srv2* (Server Core)

1. Login as **Administrator**.
2. Identify interface index:

   ```powershell
   Get-NetIPInterface
   ```
3. Enable DHCP for IPv4 (replace `4` with your **InterfaceIndex** on the Internal adapter):

   ```powershell
   Set-NetIPInterface -InterfaceIndex 4 -Dhcp Enabled
   Set-DnsClientServerAddress -InterfaceIndex 4 -ResetServerAddresses
   ipconfig /release
   ipconfig /renew
   ipconfig /all
   ```
4. Confirm **IPv4 Address = 10.0.UID.2**, **Default Gateway = 10.0.UID.1**, **DNS = 10.0.UID.1**.

### Part 2: *client1* (Windows 11)

1. **Settings > Network & Internet > Ethernet > Edit** next to **IP assignment** → **Automatic (DHCP)** → **Save**.
2. **Edit** next to **DNS server assignment** → **Automatic (DHCP)** → **Save**.
3. Command Prompt:

   ```
   ipconfig /release
   ipconfig /renew
   ipconfig /all
   ```
4. Confirm **IPv4 = 10.0.UID.11**, **Gateway 10.0.UID.1**, **DNS 10.0.UID.1**.

### Part 3: *client2* (Windows 11)

Repeat the exact steps as client1. Confirm **IPv4 = 10.0.UID.12**.

> If a machine doesn’t pick up the reserved address, re‑check the MAC you entered in the reservation and ensure the NIC you changed to DHCP is the **Internal** (HQ) adapter.

---

## Investigation 5: Verify Leases and Name Resolution

### Part 1: Check Leases in DHCP Manager

1. On *srv1*: **DHCP Manager** → **IPv4 > OSM620 HQ > Address Leases**.
2. Confirm entries for **srv2**, **client1**, **client2** with correct **Reservation** type and IPs.

### Part 2: Test DHCP + DNS

From **client1** (or **client2**):

```powershell
ipconfig /all
nslookup srv1.yourSenecaUsername.com
nslookup client2.yourSenecaUsername.com
nslookup eff.org
ping srv1.yourSenecaUsername.com
```

* All should resolve and ping (ICMP allowed per Lab 3). If `nslookup` for Internet names fails, revisit **DNS Forwarders** on *srv1*.

---

## Troubleshooting

* **Client keeps old static IP**: ensure **IP assignment = Automatic (DHCP)**; on Core, run `Set-NetIPInterface -Dhcp Enabled` then `ipconfig /release` + `/renew`.
* **Gets wrong pool address**: verify the **reservation MAC** matches the **Internal adapter**; remove/re‑add reservation if needed.
* **No default gateway**: re‑check **Option 003** in scope options.
* **DNS wrong**: verify **Option 006** points to `10.0.UID.1` and **Option 015** is your lab domain.
* **No Internet**: confirm *srv1* still NATs traffic between Internal and External (Lab 2 RRAS) and that **Forwarders** work (Lab 4).

---

## Lab 5 Sign‑Off

To complete Lab 5, show your instructor:

1. **Scope** `10.0.UID.2–199` active with Options **003**, **006**, **015** set.
2. **Reservations** for **srv2 (10.0.UID.2)**, **client1 (10.0.UID.11)**, **client2 (10.0.UID.12)**.
3. On each client, `ipconfig /all` showing **DHCP Enabled = Yes** and the correct leased address.
4. In Address Leases, entries for all three machines marked as **Reservation**.
5. `nslookup` for `srv1.yourSenecaUsername.com` **and** an Internet site returns addresses successfully.

> **You’re done.** Your lab enterprise now uses **DHCP** correctly while keeping earlier labs’ addressing and DNS intact.
