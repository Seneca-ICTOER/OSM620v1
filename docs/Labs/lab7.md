---
id: lab7
title: Lab 7 - AD Users, Groups, Computers, and GPOs
sidebar_position: 7
description: Lab 7 - AD Users, Groups, Computers, and GPOs
--- 

# Lab 7 - AD Users, Groups, Computers, and GPOs

## Lab Preparation

### Purpose of Lab 7

- In this lab, you’ll redesign and configure your environment to a more realistic, low-footprint, on-premises design. -

### Objectives

By the end of this lab, you will be able to:

- Stuff

### Minimum Progression Requirements

Before beginning, you must have:

1. **Successfully graded *Lab 6*.
1. Attended the **Week 10 - AD Users, Groups, Computers, and GPOs** lecture.
1. Your external SSD (or personal computer) with your VMs.
1. Your OSM620 Lab Logbook.
1. Optional, but recommended: Caffeine delivery system.

### Pre-Flight Check

Have the following VMs turned on:

1. router
1. srv1
1. srv2
3. srv3

## Investigation 1: Create Personal Domain Controller User

### Part 1: First OU Scaffolding Setup

1. On *srv1*, open **Active Directory Users and Computers** (ADUC).
1. Open your domain name from the list. (Example: *cjohnson30.com*)
1. Right-click your domain name and select: **New > Organizational Unit** (Do not use the built-in Users folder!)
1. Name this new OU: **HQ**
1. Using the same **New > Organizational Unit** function, create the following hierarchy:  

    > ```
    > HQ  
    > └─ Users  
    >    └─ IT  
    >       ├─ Helpdesk
    >       ├─ SecAdmins  
    >       └─ SysAdmins
    > ```

1. Verify your work. Does your HQ object hold the above items in the correct levels?
1. If so, move on to the next part. If not, fix your mistakes or ask for help.

### Part 2: Create Personal User

1. On **srv1** in ADUC, navigate to: **HQ\Users\IT\SysAdmins**
1. Right-click on *SysAdmins* (or the whitespace to the right) and select: **New > User**
1. Fill out the following in the *New Object - User* dialog box:  
    1. **First name:** *Your Proper First Name*
        > Example: Chris
    1. **Last name:** *Your Proper Last Name*
        > Example: Johnson
    1. **User login name:** *firstname.lastname*
        > Example: chris.johnson
    1. Click **Next**.
1. Fill out the following in the next page:
    1. **Password:** *same strong password as your other accounts*
    1. **Confirm password:** *same strong password as your other accounts*
    1. Check/uncheck the following:  
        1. **User must change password at next logon:** *Unchecked*
        1. **User cannot change password:** *Unchecked*
        1. **Password never expires:** *Checked*
        1. **Account is disabled:** *Unchecked*
    1. Click **Next**.
1. On the final page, review your settings and click **Finish**.

### Part 3: Add Personal User to Domain Controllers

1. On **srv1** in ADUC, navigate to: **HQ\Users\IT\SysAdmins**
1. Right-click on the user you created in Step 2 and click **Properties**.
1. In the *Properties* dialog box, click on the tab: **Member Of**
1. In the list, you should already see one entry, *Domain Users*. Click **Add**.
1. In the *Select Groups* dialog, type: **Domain Admins**
1. To verify an object named *Domain Admins* exists, click on the **Check Names** button. If it's correct, you'll see *Domain Admins* become underlined. (If not, check for typos or ask for help!)
1. Click **OK** to add.
1. Back in the *Member Of* tab, you should now see two entries. If so, click **OK** to fully apply.
1. On *srv1*, log out of your Administrator account and log back in using your new personal account by clicking on **Other user**.
    > Logging in using *firstname.lastname* should be sufficient, but if not, you can use either *SenecaID\firstname.lastname* or *<firstname.lastmane@SenecaID.com>*.
1. Open *Server Manager > All Servers* and add *srv2* and *srv3*.

You now have full domain admin access using your personal account instead of the default Administrator account. This is far more secure and best practice.

Going forward, always log into your servers using this personal account, never the default Administrator account.

### Part 4: Create a Secondary Backup Administrator

1. On **srv1** in ADUC, create a new user in: **HQ\Users\IT\SysAdmins**
1. Same steps as Part 3, but use the following values:  
    1. **Full name:** *Backup Admin*
    1. **User login name:** *backup.admin*
    1. All others the same as Part 3.
1. In this user's *Member Of*, add **Domain Admins**
1. Logout of srv1, log back in with this new user, and add *srv2/srv3* to Server Manager.
1. If the previous step worked, congrats! Keep going. If not, stop and ask for help.

### Part 5: Disable Default Administrator Account

1. On **srv1** in ADUC, nagivate to: **SenecaID.com\Users** (this is not inside HQ)
1. Find the **Administrator** account and right-click it.
1. From the drop-down menu, select: **Disable Account**

You've now disabled the default admin account and prevented a possible attack vector.

## Investigation 2: Bob from Accounting

### Part 1: Add Accounting OUs

1. On **srv1** in ADUC, navigate to: **HQ\Users**
1. Using the **New > Organizational Unit** function, ***add*** the following to your existing hierarchy:  

    > ```
    > HQ  
    > └─ Users  
    >    └─ Accountants 
    >       ├─ Managers
    >       └─ Employees
    > ```

1. Verify your work. Does your HQ object hold the above items in the correct levels?
1. If so, move on to the next part. If not, fix your mistakes or ask for help.

### Part 2: Create User - Bob Smith

1. Create a new user in the following location: **HQ\Users\Accountants\Employees**
1. Sse the following values:  
    1. **First name:** *Bob*
    1. **Last name:** *Smith*
    1. **User login name:** *bob.smith*
1. Fill out the following in the next page:
    1. **Password:** *same strong password as your other accounts*
    1. **Confirm password:** *same strong password as your other accounts*
    1. Check/uncheck the following:  
        1. **User must change password at next logon:** *Checked*
        1. **User cannot change password:** *Unchecked*
        1. **Password never expires:** *Unchecked*
        1. **Account is disabled:** *Unchecked*

### Part 3: Create GPO, *User - Employee Lockdown*

Bob from Accounting is a *terribble* user. He ignores written computer polices and likes to mess around with settings due to boredom and 'fixing things' instead of contacting IT support. So, we create a **Group Policy Object (GPO)** to disable his ability to change important system settings.

We have to create the GPO first before we can have it applied to Bob (and other users we want).

1. On *srv1*, open the **Group Policy Manager** application.
1. In the left-hand column, expand the following: **Forest: SenecaID.com > Domains > SenecaID.com > Group Policy Objects**
1. Right-click *Group Policy Objects* and select: **New**  
    1. **Name:** *User - Employee Lockdown*

### Part 4: Edit GPO, *User - Employee Lockdown*

Let's add those restrictions to our new **User - Employee Lockdown** GPO.

1. In the *Group Policy Objects* list, right-click on your newly created Group Policy Object (GPO) and click **Edit**.
1. This opens the **Group Policy Management Editor** application, and loads the **User - Employee Lockdown** GPO automatically.
1. We are now going to turn on certain restrictions.
1. Prohibit access to Control Panel and PC settings.  
    1. Nagivate to: **User Configuration > Administrative Templates > Control Panel**.
    1. Find **Prohibit access to Control Panel and PC settings** in the list and double-click it to open.
    1. Click **Enabled** then **OK** to apply.
1. Repeat for the following:  
    1. User Configuration > Policies > Administrative Templates > System > **Prevent access to the command prompt = Enabled**
    1. User Configuration > Policies > Administrative Templates > System > **Prevent access to registry editing tools = Enabled**
    1. User Configuration > Policies > Administrative Templates > Start Menu and Taskbar > **Remove Run menu from Start Menu = Enabled**
    1. User Configuration > Policies > Administrative Templates > Windows Components > File Explorer > **Remove “Map Network Drive” and “Disconnect Network Drive” = Enabled**
    1. User Configuration > Policies > Administrative Templates > Control Panel > Printers > **Prevent addition of printers = Enabled**

### Part 5: Link the *User - Employee Lockdown* GPO to Employees

Now that we have our GPO with all the restrictions added, it's time to apply it.

The best method is to apply it at the *Accounting\Employee* OU so **any** accounting employee will inherit this GPO and its restrictions, including Bob.

Much better than applying it to 50 different employees one at a time!

1. Back in the *Group Policy Manager* application, right-click on: **HQ\Users\Accounting\Employees**
1. Click **Link an existing GPO**
1. Select **User - Employee Lockdown** from the list and click **OK**.
1. You should now see it in the list in the main *Linked Group Policy Objects* pane for *Employees*. If you don't, double-check your work and ask for help before proceeding.

### Part 6: Verify Bob's Restrictions

We should check that our restrictions have worked.

1. Logout of your account on *srv1*.
1. Log in to Bob's account: **bob.smith**
    1. You will be asked to reset the password on first login. This is normal. Pick something complex but basic and **write it down in your Lab Logbook**.
1. Once logged in, try to open up **Settings**. Does it let you?
1. If not, nicely done! Move on to the next part of the lab.

This is a good example of applying settings to a user account. No matter what HQ workstation Bob logs into, these restrictions will *follow him*.

## Investigation 3: Enzo Matrix - IT Helpdesk

We're going to create a user that provides Level 1 IT support to employees in the rest of the company.

Unlike Bob, who we only needed to restrict what access he had to computers he logged into directly, with Enzo, we have to grant him specific admin privileges in Active Directory so he can manage certain things.

A Level 1 Helpdesk employee always has the same terrible job: Reset passwords for employees who have forgotten their own.

This requires some extra steps beyond what we did with Bob from Accounting.

Let's set that up.

### Part 1: Create GPO, *User - IT Environment*

The previous GPO we created is far too restrictive for an IT employee. They can be trusted to make changes to their own system.

**Remember, GPOs are about modifying *default behaviour*.** Think about when you log into a normal Windows machin you own. You can access Control Panel, right? So, to allow it here, all we need to do is **not** disable it. The default is to allow access. Same with the other restrictions we placed on the previous GPO.

Instead, we're going to add some shortcuts to the IT users' desktops for common AD management tools.

1. Open the **Group Policy Manager** and nagivate to:  **Forest: SenecaID.com > Domains > SenecaID.com > Group Policy Objects**
1. Create a new GPO here called: **User - IT Access**
1. **User Configuration > Preferences > Windows Settings > Shortcuts > *Right-Click* > New > Shortcut**
1. Add the following shortcuts:
    1. Server Manager
        1. **Name:** *Server Manager*
        1. **Location:** *Desktop*
        1. **Target Path:** *%SystemRoot%\System32\ServerManager.exe*
        1. Keep all other fields as defaults.
    1. Active Directory Users and Computers
        1. **Name:** *Active Directory Users and Computers*
        1. **Location:** *Desktop*
        1. **Target Path:** *%SystemRoot%\System32\dsa.msc*
        1. Keep all other fields as defaults.
    1. Group Policy Management
        1. **Name:** *Group Policy Management*
        1. **Location:** *Desktop*
        1. **Target Path:** *%SystemRoot%\System32\gpmc.msc*
        1. Keep all other fields as defaults.

### Part 2: Create User - Enzo Matrix

1. Create a new user in the following location: **HQ\Users\IT\Helpdesk**
1. Sse the following values:  
    1. **First name:** *Enzo*
    1. **Last name:** *Matrix*
    1. **User login name:** *enzo.matrix*
1. Fill out the following in the next page:
    1. **Password:** *same strong password as your other accounts*
    1. **Confirm password:** *same strong password as your other accounts*
    1. Check/uncheck the following:  
        1. **User must change password at next logon:** *Checked*
        1. **User cannot change password:** *Unchecked*
        1. **Password never expires:** *Unchecked*
        1. **Account is disabled:** *Unchecked*

### Part 3: Link the *User - IT Environment* GPO to Employees

Now that we have our GPO with all our additions included, it's time to apply it. We'll apply it to the *IT* OU, since it should apply to everyone there.

1. Back in the *Group Policy Manager* application, right-click on: **HQ\Users\IT**
1. Click **Link an existing GPO**
1. Select **User - IT Environment** from the list and click **OK**.
1. You should now see it in the list in the main *Linked Group Policy Objects* pane for *IT*. If you don't, double-check your work and ask for help before proceeding.

### Part 4: Global Groups

This is where we get into personal desktop environment settings VS Active Directory admin settings. GPOs are for personal desktop environments that a user sees when they login.

By contrasts, we use Global Groups+Resource Groups to grant certain AD admin tasks to groups of users.

For reference:

1. **GPO+User OU** = Desktop settings and restrictions on the local machine a user logs into.
1. **Global Groups+Resource Groups** = Combinations of AD administrative tasks assigned to groups of users. This is to allow certain users to change Active Directory settings and configuration, not local computers.

A **Global Group *(GG)*** is, essentially, an *identity group*. We use Global Groups to add users together, and then apply a role to the group. Each user in that group then gets that role applied. (We do the roles part a bit later.)

Let's create an AD admin-type group (Global Group, GG) for IT Level 1. Remember, this is just a group of users.

1. In ADOC, navigate to: **HQ**
1. Using the **New > Organizational Unit** function, ***add*** the following to your existing hierarchy:  

    > ```
    > HQ  
    > └─ Groups 
    >    └─ Global
    > ```

1. In *HQ\Groups\Global*, create a new **Group** object with the following settings:
    1. **Group name:** *GG_IT_L1*
    1. **Group scope:** *Global*
    1. **Group type:** *Security*

### Part 5: Role Groups

In contrast to Global Groups, a **Role Group *(RG)*** is a collection of AD admin privileges under a single profile. You can have many RGs, each with different sets of AD admin privileges.

Let's create our first RG and then add a single AD admin privilege to it: Reset passwords.

1. In ADOC, navigate to: **HQ**
1. Using the **New > Organizational Unit** function, ***add*** the following to your existing hierarchy:  

    > ```
    > HQ  
    > └─ Groups 
    >    └─ Roles
    > ```

1. In *HQ\Groups\Roles*, create a new **Group** object with the following settings:
    1. **Group name:** *RG_PasswordReset*
    1. **Group scope:** *Global*
    1. **Group type:** *Security*

1. In *HQ\Users\Accounting*, right-click and select: **Delegate control...**
1. In the *Delegation of Control Wizard*'s > *Users or Groups* page, add: **RG_PasswordReset**
1. In *Delegation of Control Wizard* > *Tasks to Delegate*, select: **Reset user passwords and force password change at next logon**
1. Review your settings on the last page, then click **Finish**.

### Part 6: Wire Global Group to Resource Group

We'll now assign our new RG from *Part 5* to our Global Group **GG_IT_L1**. This means that anyone who's a part of *GG_IT_L1* will get the AD admin privilege assigned in *RG_PasswordReset*.

1. In ADOC, navigate to: **HQ\Groups\Roles**
1. Double-click on **RG_PasswordReset** to open its Properties.
1. In the *Properties* window, go to the **Members** tab and click on: **Add...**
1. In the *Select Users, Contacts, Computers, Service Accounts, or Groups* window, type: **GG_IT_L1**
1. Click **OK** and verify it shows up in the *Members* tab.

The Global Group of users *GG_IT_L1* now has all the AD admin privileges given to Resource Group *RG_PasswordReset*.

### Part 7: Add Enzo to GG IT Helpdesk Level 1

And now we put it all together. We add Enzo to the Global Group *GG_IT_L1*. Once we do that, Enzo will be able to reset passwords for all users inside *HQ\Users\Accounting*.

1. In ADOC, navigate to: **HQ\Groups\Global**
1. Double-click on **GG_IT_L1** to open its Properties.
1. In the *Properties* window, go to the **Members** tab and click on: **Add...**
1. In the *Select Users, Contacts, Computers, Service Accounts, or Groups* window, type: **Enzo Matrix**
1. Click **OK** and verify it shows up in the *Members* tab.

That's it! If we ever want to add more IT employees to Helpdesk Level 1, we'd just repeat Part 7 with the new user. The rest is already setup.

### Part 8: Verify Enzo's Access and Environment

We should check that our new Enzo account works, has our user GPO applied (those desktop shortcuts), and our Helpdesk Level 1 admin access applied.

1. Logout of your account on *srv1*.
1. Log in to Enzo's account: **enzo.matrix**
    1. You will be asked to reset the password on first login. This is normal. Pick something complex but basic and **write it down in your Lab Logbook**.
1. Once logged in, try to open up **Settings**. Does it let you? It should, this time.
1. Does the desktop contain the three shortcuts we configured:
    1. **Server Manager**
    1. **Active Directory Users and Groups**
    1. **Group Policy Management**
1. If so, move on to the next part of the lab.

## Investigation 4: Dot Matrix - IT Helpdesk L2

We're going to create a user that provides **Level 2 IT support** to employees in the rest of the company.

A Level 2 Helpdesk employee has their own special AD admin privileges, along with those in Level 1.

In theory, a Level 2 Helpdesk employee shouldn't be contacted for password resets, but she may be asked to do that after completing some L2 tasks for an employee. It happens.

Fortunately, most of the work here it already done. All we need to do is create a new user, and the L2 GG and RGs.

### Part 1: Global Group - GG_IT_L2

Let's create an AD admin-type group (Global Group, GG) for IT Level 2. Remember, this is just a group of users.

1. In ADOC, navigate to: **HQ\Groups\Global** and create a new **Group** object with the following settings:
    1. **Group name:** *GG_IT_L2*
    1. **Group scope:** *Global*
    1. **Group type:** *Security*

### Part 2: Role Group - RG_OUAdmin_AllDepts

Remember, a **Role Group *(RG)*** is a collection of AD admin privileges under a single profile.

Let's create an RG that allows L2 staff to create, modify, move, and delete users in other departments.

As an example, if Bob from Accounting gets reassigned to a different department, a Level 2 specialist like Dot would be the one to move him from one department to the next in the AD structure.

Or disable his account if he gets fired. (*He is terrible, after all.*)

1. In ADOC, navigate to: **HQ\Groups\Roles** and create a new **Group** object with the following settings:
    1. **Group name:** *RG_OUAdmin_AllDepts*
    1. **Group scope:** *Global*
    1. **Group type:** *Security*

1. In *HQ\Users\Accounting*, right-click and select: **Delegate control...**
1. In the *Delegation of Control Wizard*'s > *Users or Groups* page, add: **RG_OUAdmin_AllDepts**
1. In *Delegation of Control Wizard* > *Tasks to Delegate*, select: **Create, delete, and manage user accounts**
1. Review your settings on the last page, then click **Finish**.

### Part 3: Wire Global Group to Resource Group

We'll now assign our new RG from *Part 2* to our Global Group **GG_IT_L2**. This means that anyone who's a part of *GG_IT_L2* will get the AD admin privilege assigned in *RG_PasswordReset*.

1. In ADOC, navigate to: **HQ\Groups\Roles**
1. Double-click on **RG_OUAdmin_AllDepts** to open its Properties.
1. In the *Properties* window, go to the **Members** tab and click on: **Add...**
1. In the *Select Users, Contacts, Computers, Service Accounts, or Groups* window, type: **GG_IT_L2**
1. Click **OK** and verify it shows up in the *Members* tab.

The Global Group of users *GG_IT_L2* now has all the AD admin privileges given to Resource Group *RG_OUAdmin_AllDepts*.

### Part 4: Create User - Dot Matrix

Time to create our L2 user, Dot Matrix.

1. Create a new user in the following location: **HQ\Users\IT\Helpdesk**
1. Sse the following values:  
    1. **First name:** *Dot*
    1. **Last name:** *Matrix*
    1. **User login name:** *dot.matrix*
1. Fill out the following in the next page:
    1. **Password:** *same strong password as your other accounts*
    1. **Confirm password:** *same strong password as your other accounts*
    1. Check/uncheck the following:  
        1. **User must change password at next logon:** *Checked*
        1. **User cannot change password:** *Unchecked*
        1. **Password never expires:** *Unchecked*
        1. **Account is disabled:** *Unchecked*

### Part 5: Add Dot to GG IT Helpdesk Level 1 *and* Level 2

As mentioned, a Level 2 Helpdesk staff should have L2 AD admin privileges *and* L1 AD admin privileges. **Let's add both.**

1. In ADOC, navigate to: **HQ\Groups\Global**
1. Double-click on **GG_IT_L1** to open its Properties.
1. In the *Properties* window, go to the **Members** tab and click on: **Add...**
1. In the *Select Users, Contacts, Computers, Service Accounts, or Groups* window, type: **Dot Matrix**
1. Click **OK** and verify it shows up in the *Members* tab.
1. Go back to ADOC and navigate to: **HQ\Groups\Global**
1. Double-click on **GG_IT_L2** to open its Properties.
1. In the *Properties* window, go to the **Members** tab and click on: **Add...**
1. In the *Select Users, Contacts, Computers, Service Accounts, or Groups* window, type: **Dot Matrix**
1. Click **OK** and verify it shows up in the *Members* tab.

That's it! Dot has now been granted the AD admin privileges for Level 1 ***and*** Level 2.

### Part 6: Verify Dot's Access and Environment

We should check that our new Dot account works, has our user GPO applied (those desktop shortcuts), and our Helpdesk Level 1/Level 2 admin access applied.

  > **Note:** We didn't have to do anything with GPOs this time, as we applied our IT GPO to the IT folder in Users earlier. So, when Dot was created there, she inherited that GPO. **Cool, right?**

1. Logout of your account on *srv1*.
1. Log in to Dot's account: **dot.matrix**
    1. You will be asked to reset the password on first login. This is normal. Pick something complex but basic and **write it down in your Lab Logbook**.
1. Once logged in, try to open up **Settings**. Does it let you? It should, this time.
1. Does the desktop contain the three shortcuts we configured:
    1. **Server Manager**
    1. **Active Directory Users and Groups**
    1. **Group Policy Management**
1. If so, move on to the next part of the lab.
