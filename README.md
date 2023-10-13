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

![Image](https://i.imgur.com/4r6vDVs.png)

Login to CLIENT as John_Admin and head to sytem agian, Remote Desktop, Select users that can remotiley access this PC, ADD, type Domain Users, Check names, OK, OK. Now every user under Domain Users can log into CLIENT. 

Login to CLIENT as John_Admin and head to **System** again. Navigate to **Remote Desktop**, select **Users that can remotely access this PC**, click **ADD**, type "Domain Users," then click **Check names** and **OK** x2. Now, every user under Domain Users can log into CLIENT.

![Image](https://i.imgur.com/oGrEjCy.png)

To populate our users for the sake of experimentation, open Windows PowerShell ISE as an administrator on DC-1 under the user John_Admin. Create a new file and paste this [script](https://github.com/NicholasToon/Configuring-On-premises-Active-Directory-within-Azure-VMs/files/12896330/Code.txt) (I did not create this code; credit goes to [joshmadakor1](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)) into the console. You may want to tweak the number of accounts to create a smaller value to avoid continuous generation while you proceed with the rest of this tutorial. You can also adjust the password as desired. Once the script is configured to your liking, run it and observe the generation of the accounts. Please be aware that due to the random generation method of this script, there is a potential chance of NSFW (Not Safe for Work) names being generated.

![Image](https://i.imgur.com/CkzRTpU.png)

If you want to create some users manually, that is also possible. Simply create a new organizational unit by the name of "_EMPLOYEES," open the folder, right-click, choose **New**, then **User**. Fill out the information just as we did for the admin user. Use that login for CLIENT. As for the randomly generated users, you can choose any one of them to log in on CLIENT as seen above.

![Image](https://i.imgur.com/3V1dhOc.png) 


If at any point you created a file like an Orgizational unit (for e.g.) that you can't delete because it was generated with the Protect container from accidental deletion box clicked then I will show you how to rectify the problem. 

Press start, search and open Actice Directory Administrative Center, switch to tree view, right click on the offending files, properties, uncheck Protect container from accidental deletion box, OK, right click again, and delete. The file will no longer exist. 






