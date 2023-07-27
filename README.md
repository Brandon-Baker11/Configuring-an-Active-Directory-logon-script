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
In this lab, we will set up a script that will automatically run for the user we will create on our domain controller. Logon scripts can be used for several purposes, such as mapping network drives to users and computers, installing applications, and setting up printers. Today we will be creating a script that will map a shared folder to our user. Once the script is written, it will need to be saved to a batch file. We will then create a shared folder using the Group Policy Editor and use Windows Powershell to force an update of the group policy.
