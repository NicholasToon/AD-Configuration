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

We will now grant John Doe administrative privileges. Right-click on the user, go to **Properties**, select the **Member Of** tab, click **Add**, choose the security group for your user by typing it in the box (in John Doe's case it will be **Domain Admins**), click **Check Names**, then **OK**, **Apply**, and finally **OK**. From this point forward, we will use the admin account to make any further changes. Sign out and then back in to the RDC as John_Admin (remember to keep track of your credentials). You can use the command line while on DC-1 and type in **Whoami**. As the command states, it will display the name of the current user, who at this point should be John_Admin.

![Image](https://i.imgur.com/iTxBkcR.png)

To simulate the general connection process of a computer on a standard system, we first need to join the **CLIENT** to the **Domain Controller**. Start by joining CLIENT with the base Labuser credentials. To change the domain, right-click on Start, go to **System**, then select **Rename this PC (advanced)**. Click **Change**, choose **Domain**, and enter your chosen domain. Typically, this would attempt to communicate with a random domain matching our input on the web and fail, but because we changed the DNS settings of CLIENT in the previous tutorial, we will be able to successfully join. Click **OK**, enter the admin account credentials we created. Click **OK**, **OK**, and finally **OK** one last time when asked to restart, and then select **Restart Now**.

The CLIENT will now be listed under **Computer** in the **Active Directory Users and Computers** panel and is accessible by Domain Admins, even though John_Admin has never logged into CLIENT. However, we want all domain users to have access to CLIENT.

![Image](








