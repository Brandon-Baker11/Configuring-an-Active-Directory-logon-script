![what-is-active-directory-and-why-is-it-used](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/1ab31f15-f765-49e3-bdab-8e8704eecb6c)

# Configuring an Active Directory logon script (OracleVM VirtualBox)
This tutorial will outline the implementation of a logon script using Active Directory within a VirtualBox VM

## Environments and Technologies Used
- OracleVM VirtualBox
- Active Directory Domain Services
- Batch files
- Group Policy Editor
- Windows PowerShell

## Operating Systems Used
- Windows Server 2019
- Windows 10 (22H2)

## Configuration Steps
In this lab, we will set up a script that will automatically run for the user we will create on our domain controller (DC). Logon scripts can be used for several purposes, such as mapping network drives to users and computers, installing applications, and setting up printers. Today we will be creating a script that will map a shared folder to our user. Once the script is written, it will need to be saved to a batch file. We will then create a shared folder using the Group Policy Editor and use Windows Powershell to force an update of the group policy.


Okay, so we are going to log into our DC as an administrator, and we will open the server manager application and select ***Tools*** in the top right-hand corner, and then select ***Active Directory Users and Computers*** from the drop down menu.
![Screenshot1](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/34ef2feb-a39c-445c-9eba-700cccfb655c)


In the ***Active Directory Users and Computers*** window, right-click any blank space there is in the details pane to the right and select ***New*** and then select ***Group***
![Screenshot0](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/f72f086c-a053-4187-b3c4-3f215aa6679b)


In the ***New Object-Group*** dialogue box, type "Folder Redirect" into the ***Group name*** field

Click ***OK***
![Screenshot01](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/58244e12-7942-4fac-aec6-041bee14ca5b)


In the ***Active Directory Users and Computers*** window, right-click any blank space there is in the details pane to the right and select ***New*** and then select ***User***
![Screenshot2](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/8b6f7e89-87a2-4e0a-a7d8-1c5172cac459)


In the ***New Object-User*** dialogue box, type "testuser" into the ***First name*** and ***User logon name*** fields

Click ***Next***
![Screenshot3](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/27827024-dfe7-4078-a002-d07479d0f721)


Type "Password1" into the ***Password*** and ***Confirm Password fields (This isn't the strongest password I know, but this is just for demonstration purposes). Then disable ***User must change password at next logon*** and enable ***Password never expires*** 

Click ***Next***
![Screenshot4](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/6c082d30-cae2-4e0f-a86b-251c14c29172)


Click ***Finish***
![Screenshot5](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/e1cefbfe-e931-48f9-ab74-fc5e9cdc61d2)


Now, back on the ***Active Directory Users and Computers*** window, right-click the group we just created, ***Folder Redirect*** and select ***Properties***
![Screenshot6](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/8c3ec0a6-d362-498b-b377-8c0d9d463c3f)


From the ***Folder Redirect Properties*** dialogue box, select the ***Members*** tab and click ***Add***
![Screenshot7](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/a4e87993-daf7-4f7c-b84e-e6174ed873cd)


In the ***Select Users, Contacts, Computers, Service Accounts, or Groups*** dialogue box, type "testuser" in the ***Enter the object names to select*** field and click ***Check Names*** and click ***OK***
> The user's username will populate once you click the ***Check Names*** button
![Screenshot8](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/3de5519a-d83a-4625-b83e-958762559fba)


The user ***testuser*** is now added as a member of the ***Folder Redirect*** group

Click ***OK***
![Screenshot9](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/e8492b10-beb3-4632-bdad-da6619c6dd71)





































