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


<!--In the ***Active Directory Users and Computers*** window, right-click any blank space there is in the details pane to the right and select ***New*** and then select ***Group***
![Screenshot0](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/f72f086c-a053-4187-b3c4-3f215aa6679b)


In the ***New Object-Group*** dialogue box, type "Folder Redirect" into the ***Group name*** field

Click ***OK***
![Screenshot01](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/58244e12-7942-4fac-aec6-041bee14ca5b)-->


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


<!--Now, back on the ***Active Directory Users and Computers*** window, right-click the group we just created, ***Folder Redirect*** and select ***Properties***
![Screenshot6](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/8c3ec0a6-d362-498b-b377-8c0d9d463c3f)


From the ***Folder Redirect Properties*** dialogue box, select the ***Members*** tab and click ***Add***
![Screenshot7](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/a4e87993-daf7-4f7c-b84e-e6174ed873cd)


In the ***Select Users, Contacts, Computers, Service Accounts, or Groups*** dialogue box, type "testuser" in the ***Enter the object names to select*** field and click ***Check Names*** and click ***OK***
> The user's username will populate once you click the ***Check Names*** button
![Screenshot8](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/3de5519a-d83a-4625-b83e-958762559fba)


The user ***testuser*** is now added as a member of the ***Folder Redirect*** group

Click ***OK***
![Screenshot9](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/e8492b10-beb3-4632-bdad-da6619c6dd71) -->


Next, we are going to make the folder that we intend to map to the user everytime they log in. Open file explorer and click ***This PC*** and then double-click ***Local Disk (C:)***
![Screenshot10](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/933dd252-968a-4e3e-8649-43f558d0e255)


Right-click anywhere in the details pane to the right, click ***New*** > ***Folder***
![Screenshot11](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/eca7e236-5a5f-49c8-9cbb-f53ebec6b8c3)


Next, right-click ***New Folder*** and select ***Rename*** and name it "Share"
![Screenshot12](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/fca69e15-3305-4e5e-a981-c60ac1b0f13e)


Right-click on the ***Share*** folder we just made and select ***Properties***
![Screenshot13](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/c1b69964-ac19-46f8-aaf0-a0d12e11eb42)


In the ***Share Properties*** dialogue box, select the ***Sharing*** tab at the top
![Screenshot14](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/8ff769e5-e942-4b03-8dcb-7b783e617030)


And now from the ***Sharing*** tab, select ***Advanced Sharing*** 
![Screenshot15](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/68fd2e17-02fa-4985-99f2-a223671a0200)


In the ***Advanced Sharing*** dialogue box, enable the ***Share this folder*** checkbox
![Screenshot16](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/96717e9d-9e24-4732-bc75-829bef2f85a8)


In the ***Advanced Sharing*** dialogue box select ***Permissions***
![Screenshot17](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/b87df3f8-435f-45c9-9c6b-b80790191659)


In the ***Permissions for Share*** dialogue box click ***Add...***
![Screenshot18](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/5e50fd26-c535-42d5-9c12-b30bbad4bc51)


In the ***Select Users, Contacts, Computers, Service Accounts, or Groups*** dialogue box, type "testuser" and click ***Check Names*** and the username for our created user will populate in the field

Click ***OK***
![Screenshot19](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/7feabb2c-b5aa-49a0-a0e7-20a03fd3b086)


Now, from the ***Permissions for Share*** dialogue box, make sure ***testuser*** is selected and under ***Permissions for testuser*** allow ***Full Control***

Click ***OK***
![Screenshot20](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/66fcea29-8033-4759-95ac-293a5a25ba90)


We have just created the folder that we will connect to everytime testuser logs in. Click ***OK*** on the ***Advanced Sharing*** dialogue box and the click ***Close*** in the ***Share Properties*** dialogue box
![Screenshot21](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/1713bbd3-07ee-4546-bdbe-7a86a35334ac)


We will now create a batch file that will complete the mapping process for us automatically. A batch file is commonly used to back up files, process logs, diagnostics, and other common administrative tasks. To create a batch file, a text editor will be used, and the script will be written


Now click the search icon in your taskbar and type "Notepad" and select the ***Notepad*** application from the best match results
![Screenshot22](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/f7dda5b1-2bcd-4f38-aa88-7d2946d9819e)


In the ***Untitled-Notepad*** window type ***net use x: \\\DC\Share***. Notice with this command we are:
1. Using the ***net use*** command to access resources that are on the DC's network
2. Identifying the drive letter ***x:*** to be mapped to this folder
3. And stating the path where the folder we want to share is located ***\\\DC*** being the server it is located at and ***\Share*** being the folder that we want to access
![Screenshot23](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/5abd96ba-5130-41c0-8c88-197b21404120)


Now, click ***File*** in the top left and select ***Save as***
![Screenshot24](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/219d4375-7ba3-4e2a-9217-5ba8f8e322c2)


We are going to save it on the ***Desktop*** so it's easy to find. Then name the script file ***XShare.bat***

Click ***Save***
![Screenshot25](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/c22b7dbc-af20-4f70-a406-224c257c80f6)


<!--Close the ***NotePad*** window and minimize any other windows that are open and you'll see that our batch file is saved onto the desktop. Right-click ***XShare.bat*** and select ***Run as Administrator
![Screenshot26](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/9315ae38-4fc7-48d3-96a7-fc81d144858d)


If a ***User Account Control*** prompt pops up asking for permission to run the program, click ***Yes*** or type in your administrator credentials to allow the script to be automatically run in the command line
![Screenshot27](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/bc3f8698-b2b0-4b92-887c-675fe629ea9f)


Now refocus the ***File Explorer*** window and select ***This PC*** in the left-hand pane and notice that the script created the ***Share*** under network locations
![Screenshot28](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/52502f32-0486-4811-a1b2-397ea0b39f71) -->
























