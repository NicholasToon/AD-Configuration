![Image](https://i.imgur.com/I4b2apl.png)

## Active Directory Configuration 
In this AD configuration, we will cover the creation of an administrative account, the setup of multiple user accounts, and the configuration of Remote Desktop for these users, among other related tasks.

## Environments and Technologies Used 

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection (RDC)
- Active Directory Domain Services
- Windows PowerShell

## Operatiing Systems Used

- Windows Server 2022
- Windows 10 Pro (22H2)

## Configuration

![Image](https://i.imgur.com/xGh03cZ.png)

We will begin by creating new **Organizational Units** and users inside the **Server Manager Dashboard** on our DC-1. Click on **Tools**, then **Active Directory Users and Computers**. Right-click on your chosen domain (for my this scenario, it's mydomain.com), select **New**, and then **Organizational Unit**. Create two units: one called "_EMPLOYEES" and the other called "_ADMINS." Creating them in this format will help with identification and selection, both now and in the future. 

![Image](https://i.imgur.com/yt5loj4.png)

Inside the **_ADMINS** **Organizational Unit**, create a new user named John Doe. Unselect the option **User must change password at the next login** and select **Password never expires** to avoid future complications. Give it a password and **Finish** the user generation.

![Image](https://i.imgur.com/WBbwsj6.png)

We will now grant John Doe administrative privileges. Right-click on the user, go to **Properties**, select the **Member Of** tab, click **Add**, choose the security group for your user by typing it in the box (in John Doe's case it will be **Domain Admins**), click **Check Names**, then **OK**, **Apply**, and finally **OK**. From this point forward, we will use the admin account to make any further changes. Sign out and then back in to the RDC as John_Admin (remember to keep track of your credentials).


