![what-is-active-directory-and-why-is-it-used](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/1ab31f15-f765-49e3-bdab-8e8704eecb6c)

# Configuring an Active Directory logon script (OracleVM VirtualBox)
This tutorial will outline the implementation of a logon script using Active Directory within a VirtualBox VM

## Environments and Technologies Used
- OracleVM VirtualBox
- Active Directory Domain Services
- Batch files
- Group Policy Management
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


Now restore the ***File Explorer*** window and select ***This PC*** in the left-hand pane and notice that the script created the ***Share*** under network locations
![Screenshot28](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/52502f32-0486-4811-a1b2-397ea0b39f71) -->


Next we will be creating the Group Policy Object for the script that we just created. Restore the ***Server Manager*** window and click ***Tools*** and then select ***Group Policy Management***
![Screenshot29](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/6e1ae095-5bde-46ad-8f14-a991cd716078)


In the ***Group Policy Management*** window right-click ***Group Policy Objects*** and click ***New***
![Screenshot30](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/b2dd3cd1-fdb0-47c3-9885-e57212097255)

In the ***New GPO*** pop-up, name the object ***XShare Logon Script GPO***

Click ***OK***
![Screenshot31](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/ea9cd782-0b88-455d-928a-2e09f2b48feb)


Back on the ***Group Policy Management*** window, right-click ***XShare Logon Script GPO*** and select ***Edit***
![Screenshot32](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/84ed437b-fd7b-4aa6-bcf2-244e675ae62f)


On the ***Group Policy Management Editor*** window expand ***User configuration > Policies > Windows Settings*** select ***Scripts (Logon/Logoff)***
![Screenshot33](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/30639fc0-1672-44d8-8453-a30dec54dfd8)


Now in the ***Scripts (Login/Logoff)*** pane right-click ***Logon*** and select ***Properties***
![Screenshot34](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/94db04b9-d23e-4987-86de-8571c6594668)


From the ***Logon Properties*** window select ***Show Files***. The ***Logon*** window will be empty, what we will do is restore the ***File Explorer*** window and copy our ***XShare*** script we saved to the desktop and paste it to the ***Logon*** File Explorer window

Close the ***Logon*** File Explorer window and restore the ***Group Policy Management Editor*** window from the taskbar
![Screenshot35](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/81af6c76-f51a-4c95-bfa2-0696e1fd7693)


In the ***Logon Properties*** window click ***Add*** and then click ***Browse*** and in the ***Browse*** dialogue box select ***XShare***

Click ***OK***
![Screenshot36](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/adcdc458-e913-4e34-92bc-3ed4df65c6a7)


Now, inside the ***Logon Properties*** dialogue box you see that XShare has been added as a logon script
![Screenshot37](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/c84c5337-ccd6-473d-935a-100c6581b8cf)


You can close ***Group Policy Management Editor*** and restore the ***Group Policy Management*** window and expand ***Group Policy Objects*** and select ***XShare Logon Script GPO*** and under ***Security Filtering*** in the right pane click ***Add***
![Screenshot38](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/752554d1-2fa7-4dee-b4e2-7671bb556f30)


In the ***Select User, Computer, or Group*** dialogue box, enter the name "testuser" in the ***Enter the object name to select*** field and click ***Check Names***

Click ***OK***
And now ***testuser*** has been added to ***XShare Logon Script GPO*** 
![Screenshot39](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/7a23e9a7-d9b1-4109-8ab9-52711989736e)


Now right-click on the name of your domain in the left pane and select ***Link Existing GPO*** and in the ***Select GPO*** window select ***XShare Logon Script GPO***

Click ***OK***
![Screenshot40](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/239d1ee4-70cd-4402-8ae5-03ecb19742f1)


Now we will log into our ***testuser*** account on our client machine and update the Group Policy. Once you're logged in, right-click the Windows ***Start*** charm and select ***Windows PowerShell (Admin)***
![Screenshot41](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/75265941-d9b0-450c-a39f-fea5e796d229)


If you would like to see the things you could do with the gpupdate command type ***gpupdate /?*** but for now, we will use the command ***gpupdate /force*** to apply any changes that have taken place and press enter. Once you are done you will see PowerShell tell you that the computer and user policy updates were completed successfully
![Screenshot42](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/b7ac2667-77cd-4261-8045-5058fff914df)


Now, type the command ***gpresult /r*** into PowerShell and press enter. This will display all of the policies that have changed and the objects they were applied to

If you get a ***no user data in RSoP*** error close the ***PowerShell*** window and reopen it with standard permissions and it should work
![Screenshot43](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/e39f5ce2-0641-4863-823a-b928bad95d48)


Now open ***File Explorer*** from the taskbar and click ***This PC*** and in the details pane to the right, you should see ***Share (\\\DC) (X:)*** under ***Network locations***
![Screenshot44](https://github.com/Brandon-Baker11/Configuring-an-Active-Directory-logon-script/assets/140644499/9a6e225c-5354-42cf-b676-5abb63671295)






















