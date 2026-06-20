## INTRODUCTION TO WINDOWS

Microsoft first introduced the Windows operating system on November 20, 1985.

### Windows Versions

| Operating System Name                | Version Number |
| ------------------------------------ | -------------- |
| Windows NT 4                         | 4.0            |
| Windows 2000                         | 5.0            |
| WIndows XP                           | 5.1            |
| Windows Server 2003                  | 5.2            |
| Windows Vista, Server 2008           | 6.0            |
| Windows 7, Server 2008 R2            | 6.1            |
| Windows 8, Server 2012               | 6.2            |
| Windows 8.1, Server 2012 R2          | 6.3            |
| Windows 10, Server 2016, Server 2019 | 10.0           |
We can use the [Get-WmiObject](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.management/get-wmiobject?view=powershell-5.1) [cmdlet](https://docs.microsoft.com/en-us/powershell/scripting/developer/cmdlet/cmdlet-overview?view=powershell-7) to find information about the operating system.

### Remote Access Protocol
Port 3389. Arquitectura client-servidor.
Per a que funcioni s'ha d'activar prèviament a Windows.

## CORE OF THE OPERATING SYSTEM
### Operating System Structure

| DIRECTORY                  | FUNCTION                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Perflogs                   | Can hold Windows performance logs but is empty by default.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| Program Files              | 32-bit and 16-bit programs are installed here on 64-bit editions of Windows.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ProgramData                | This is a hidden folder that contains data that is essential for certain installed programs to run. This data is accessible by the program no matter what user is running it.                                                                                                                                                                                                                                                                                                                                                                                  |
| Users                      | This folder contains user profiles for each user that logs onto the system and contains the two folders Public and Default.                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| Default                    | This is the default user profile template for all created users. Whenever a new user is added to the system, their profile is based on the Default profile.                                                                                                                                                                                                                                                                                                                                                                                                    |
| Public                     | This folder is intended for computer users to share files and is accessible to all users by default. This folder is shared over the network by default but requires a valid network account to access.                                                                                                                                                                                                                                                                                                                                                         |
| AppData                    | Per user application data and settings are stored in a hidden user subfolder (i.e., cliff.moore\AppData). Each of these folders contains three subfolders. The Roaming folder contains machine-independent data that should follow the user's profile, such as custom dictionaries. The Local folder is specific to the computer itself and is never synchronized across the network. LocalLow is similar to the Local folder, but it has a lower data integrity level. Therefore it can be used, for example, by a web browser set to protected or safe mode. |
| Windows                    | The majority of the files required for the Windows operating system are contained here.                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| System, System32, SysWOW64 | Contains all DLLs required for the core features of Windows and the Windows API. The operating system searches these folders any time a program asks to load a DLL without specifying an absolute path.                                                                                                                                                                                                                                                                                                                                                        |
| WinSxS                     | The Windows Component Store contains a copy of all Windows components, updates, and service packs.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
*Comandes explicades: dir, tree*

## FILE SYSTEM
There are 5 types of Windows file systems: FAT12, FAT16, FAT32, NTFS, and exFAT. FAT12 and FAT16 are no longer used on modern Windows operating systems. We will touch upon the FAT32 and exFAT file systems for this training, but our main focus will be the NTFS file system.

The "32" in the name refers to the fact that FAT32 uses 32 bits of data for identifying data clusters on a storage device.


| PROS OF FAT32                                                                                                                                       | CONS OF FAT32                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Device compatibility - it can be used on computers, digital cameras, gaming consoles, smartphones, tablets, and more.                               | Can only be used with files that are less than 4GB.       |
| Operating system cross-compatibility - It works on all Windows operating systems starting from Windows 95 and is also supported by MacOS and Linux. | No built-in data protection or file compression features. |
|                                                                                                                                                     | Must use third-party tools for file encryption.           |

| PROS OF NTFS                                                                                                        | CONS OF NTFS                                                                                       |
| ------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| NTFS is reliable and can restore the consistency of the file system in the event of a system failure or power loss. | Most mobile devices do not support NTFS natively.                                                  |
| Provides security by allowing us to set granular permissions on both files and folders.                             | Older media devices such as TVs and digital cameras do not offer support for NTFS storage devices. |
| Supports very large-sized partitions.                                                                               |                                                                                                    |
| Has journaling built-in, meaning that file modifications (addition, modification, deletion) are logged.             |                                                                                                    |

### Permissions NTFS
The NTFS file system has many basic and advanced permissions.

| PERMISSION TYPE      | DESCRIPTION                                                                                                                |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| Full Control         | Allows reading, writing, changing, deleting of files/folders.                                                              |
| Modify               | Allows reading, writing, and deleting of files/folders.                                                                    |
| List Folder Contents | Allows for viewing and listing folders and subfolders as well as executing files. Folders only inherit this permission.    |
| Read and Execute     | Allows for viewing and listing files and subfolders as well as executing files. Files and folders inherit this permission. |
| Write                | Allows for adding files to folders and subfolders and writing to a file.                                                   |
| Read                 | Allows for viewing and listing of folders and subfolders and viewing a file's contents.                                    |
| Traverse Folder      | This allows or denies the ability to move through folders to reach other files or folders.                                 |
### Integrity Controll Access Control Lists (icacls)
NTFS permissions on files and folders in Windows can be managed using the File Explorer GUI under the security tab. Apart from the GUI, we can also achieve a fine level of granularity over NTFS file permissions in Windows from the command line using the icacls utility.

We can list out the NTFS permissions on a specific directory by running either `icacls` from within the working directory or `icacls C:\Windows` against a directory not currently in.

![[Pasted image 20260620145335.png]]

The possible inheritance settings are:
- `(CI)`: container inherit
- `(OI)`: object inherit
- `(IO)`: inherit only
- `(NP)`: do not propagate inherit
- `(I)`: permission inherited from parent container

Basic access permissions are as follows:
- `F` : full access
- `D` :  delete access
- `N` :  no access
- `M` :  modify access
- `RX` :  read and execute access
- `R` :  read-only access
- `W` :  write-only access

A full listing of `icacls` command-line arguments and detailed permission settings can be found [here](https://ss64.com/nt/icacls.html).

### NTFS vs Share Permissions

The `Server Message Block protocol` (`SMB`) is used in Windows to connect shared resources like files and printers. It is used in large, medium, and small enterprise environments.

![[Pasted image 20260620145555.png]]

#### Share permissions

| PERMISSION   | DESCRIPTION                                                                                                                                 |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------- |
| Full Control | Users are permitted to perform all actions given by Change and Read permissions as well as change permissions for NTFS files and subfolders |
| Change       | Users are permitted to read, edit, delete and add files and subfolders                                                                      |
| Read         | Users are allowed to view file & subfolder contents                                                                                         |
![[Pasted image 20260620145842.png]]

![[Pasted image 20260620145900.png]]

#### Comandes smbclient

| COMMAND                                             | DESCRIPTION                              |
| --------------------------------------------------- | ---------------------------------------- |
| smbclient -L SERVER_IP -U htb-student               | Using smbclient to list available shares |
| smbclient '\\SERVER_IP\Company Data' -U htb-student | Connecting to the Company Data share     |

## WORKING WITH SERVICES AND PROCESSES
### WINDOWS SERVICES AND PROCESSES
#### Services
Services are a major component of the Windows operating system. They allow for the creation and management of long-running processes. Windows services can be started automatically at system boot without user intervention. These services can continue to run in the background even after the user logs out of their account on the system.

Windows services are managed via the Service Control Manager (SCM) system, accessible via the `services.msc` MMC add-in.

In Windows, we have some [critical system services](https://docs.microsoft.com/en-us/windows/win32/rstmgr/critical-system-services) that cannot be stopped and restarted without a system restart.


| SERVICE                   | DESCRIPTION                                                                                                                                                                                                                                             |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| smss.exe                  | Session Manager SubSystem. Responsible for handling sessions on the system.                                                                                                                                                                             |
| csrss.exe                 | Client Server Runtime Process. The user-mode portion of the Windows subsystem.                                                                                                                                                                          |
| wininit.exe               | Starts the Wininit file .ini file that lists all of the changes to be made to Windows when the computer is restarted after installing a program.                                                                                                        |
| logonui.exe               | Used for facilitating user login into a PC                                                                                                                                                                                                              |
| lsass.exe                 | The Local Security Authentication Server verifies the validity of user logons to a PC or server. It generates the process responsible for authenticating users for the Winlogon service.                                                                |
| services.exe              | Manages the operation of starting and stopping services.                                                                                                                                                                                                |
| winlogon.exe              | Responsible for handling the secure attention sequence, loading a user profile on logon, and locking the computer when a screensaver is running.                                                                                                        |
| System                    | A background system process that runs the Windows kernel.                                                                                                                                                                                               |
| svchost.exe with RPCSS    | Manages system services that run from dynamic-link libraries (files with the extension .dll) such as "Automatic Updates," "Windows Firewall," and "Plug and Play." Uses the Remote Procedure Call (RPC) Service (RPCSS).                                |
| svchost.exe with Dcom/PnP | Manages system services that run from dynamic-link libraries (files with the extension .dll) such as "Automatic Updates," "Windows Firewall," and "Plug and Play." Uses the Distributed Component Object Model (DCOM) and Plug and Play (PnP) services. |
This [link](https://en.wikipedia.org/wiki/List_of_Microsoft_Windows_components#Services) has a list of Windows components, including key services.

#### Processes
Processes run in the background on Windows systems. They either run automatically as part of the Windows operating system or are started by other installed applications.

Certain processes are critical and, if terminated, will stop certain components of the operating system from running properly.

#### Local Security Authority Subsystem Service (LSASS)
`lsass.exe` is the process that is responsible for enforcing the security policy on Windows systems.

When a user attempts to log on to the system, this process verifies their log on attempt and creates access tokens based on the user's permission levels. That's why LSASS is on extremly target as several tools exist to extract both cleartext and hashed credentials sotred in memory by this process.

All events associated with this process (logon/logoff attempts, etc.) are logged within the Windows Security Log.

#### Sysinternals Tools
The [SysInternals Tools suite](https://docs.microsoft.com/en-us/sysinternals) is a set of portable Windows applications that can be used to administer Windows systems.

We can run procdump.exe directly from this share without downloading it directly to disk.

![[Pasted image 20260620150926.png]]

The suite include tools that can be used to monitor file system, registry, and network activity related to any process running on the system.

### SERVICE PERMISSION

Service permissions misconfigurations put in place by 3rd party software and easy to make mistakes by admins during install process.

It is highly recommended to create an individual user account to run critical network services. These are refunded to as service accounts.

#### Examining services using services.msc
![[Pasted image 20260620151329.png]]

We can use services.msc to view and manage just about every detail regarding all services.

"Path to the executable" is the full path to the program and command to execute when the service starts.

#### Examining services using sc

sc gives us the ability to quickly search and analyze commonly targeted services and newly created services.

![[Pasted image 20260620151622.png]]

![[Pasted image 20260620154205.png]]

Every named object in Windows is a [securable object](https://docs.microsoft.com/en-us/windows/win32/secauthz/securable-objects), and even some unnamed objects are securable. If it's securable in a Windows OS, it will have a [security descriptor](https://docs.microsoft.com/en-us/windows/win32/secauthz/security-descriptors). Security descriptors identify the object’s owner and a primary group containing a `Discretionary Access Control List` (`DACL`) and a `System Access Control List` (`SACL`).

We can query a service over the network:

![[Pasted image 20260620154320.png]]


#### Examine service permissions using Powershell
Using the `Get-Acl` PowerShell cmdlet, we can examine service permissions by targeting the path of a specific service in the registry.

![[Pasted image 20260620154808.png]]

### WINDOWS SESSIONS (NON-INTERACTIVE)

Non-interactive accounts does not require login credentials. There are three types of non-interactive accounts:

| ACCOUNT               | DESCRIPTION                                                                                                                                                                                                                                                            |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Local System Account  | Also known as the `NT AUTHORITY\SYSTEM` account, this is the most powerful account in Windows systems. It is used for a variety of OS-related tasks, such as starting Windows services. This account is more powerful than accounts in the local administrators group. |
| Local Service Account | Known as the `NT AUTHORITY\LocalService` account, this is a less privileged version of the SYSTEM account and has similar privileges to a local user account. It is granted limited functionality and can start some services.                                         |
| Local Service Account | This is known as the `NT AUTHORITY\NetworkService` account and is similar to a standard domain user account. It has similar privileges to the Local Service Account on the local machine. It can establish authenticated sessions for certain network services.        |

### INTERACTING WITH THE WINDOWS OS
#### Remote Desktop Protocol
[RDP](https://support.microsoft.com/en-us/help/186607/understanding-the-remote-desktop-protocol-rdp) is a proprietary Microsoft protocol which allows a user to connect to a remote system over a network connection and obtain a graphical user interface.

RDP uses port 3389

#### The Command Prompt (CMD)

`C:\Windows\system32\cmd.exe`

Generalment `help <command>`

Però algunes comandes `<command> /?`


#### Powershell

**CMDLET** 
- Small single-function tools built into the shell designed to perform specific tasks. There are more than 100 core cmdlets. 
- Cmdlets are in form of Verb-Noun.

ALIASES
- Son abreviatures dels cmdlets
- Podem crear les nostres abreviatures personalitzades

![[Pasted image 20260620155800.png]]

#### Execution Policy
Sometimes we wil find that we are unable to run scripts on a a system. This is due to a security feature called the 'execution policy', which attempts to prevent the execution of malicious scripts.

| **POLICY**     | **DESCRIPTION**                                                                                                                                                                                                                                                  |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `AllSigned`    | All scripts can run, but a trusted publisher must sign scripts and configuration files. This includes both remote and local scripts. We receive a prompt before running scripts signed by publishers that we have not yet listed as either trusted or untrusted. |
| `Bypass`       | No scripts or configuration files are blocked, and the user receives no warnings or prompts.                                                                                                                                                                     |
| `Default`      | This sets the default execution policy, `Restricted` for Windows desktop machines and `RemoteSigned` for Windows servers.                                                                                                                                        |
| `RemoteSigned` | Scripts can run but requires a digital signature on scripts that are downloaded from the internet. Digital signatures are not required for scripts that are written locally.                                                                                     |
| `Restricted`   | This allows individual commands but does not allow scripts to be run. All script file types, including configuration files (`.ps1xml`), module script files (`.psm1`), and PowerShell profiles (`.ps1`) are blocked.                                             |
| `Undefined`    | No execution policy is set for the current scope. If the execution policy for ALL scopes is set to undefined, then the default execution policy of `Restricted` will be used.                                                                                    |
| `Unrestricted` | This is the default execution policy for non-Windows computers, and it cannot be changed. This policy allows for unsigned scripts to be run but warns the user before running scripts that are not from the local intranet zone.                                 |

`Get-ExecutionPolicy -List`
![[Pasted image 20260620160027.png]]


### WINDOWS MANAGEMENT INSTRUMENTATION

WMI is a subsystem of PowerShell that provides system administrators with powerful tools for system monitoring.

| **COMPONENT NAME** | **DESCRIPTION**                                                                                                                                                                    |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| WMI service        | The Windows Management Instrumentation process, which runs automatically at boot and acts as an intermediary between WMI providers, the WMI repository, and managing applications. |
| Managed objects    | Any logical or physical components that can be managed by WMI.                                                                                                                     |
| WMI providers      | Objects that monitor events/data related to a specific object.                                                                                                                     |
| Classes            | These are used by the WMI providers to pass data to the WMI service.                                                                                                               |
| Methods            | These are attached to classes and allow actions to be performed. For example, methods can be used to start/stop processes on remote machines.                                      |
| WMI repository     | A database that stores all static data related to WMI.                                                                                                                             |
| CIM Object Manager | The system that requests data from WMI providers and returns it to the application requesting it.                                                                                  |
| WMI API            | Enables applications to access the WMI infrastructure.                                                                                                                             |
| WMI Consumer       | Sends queries to objects via the CIM Object Manager.                                                                                                                               |
Some of the uses for WMI are:
- Status information for local/remote systems
- Configuring security settings on remote machines/applications
- Setting and changing user and group permissions
- Setting/modifying system properties
- Code execution
- Scheduling processes
- Setting up logging

WMI can be used with powershell by using `Get-WmiObject` module.

Laters sections will show some ways that WMI can be leveraged offensively for both enumeration and lateral movement.


### MICROSOFT MANAGEMENT CONSOLE (MMC)

The MMC can be used to group snap-ins, or administrative tools, to manage hardware, software, and network components within a Windows host.

![[Pasted image 20260620160511.png]]

We can save the set of snap-ins as a .msc file, so they will all be loaded the next time we open MMC.

![[Pasted image 20260620160642.png]]

### WINDOWS SUBSYSTEM FOR LINUX (WSL)

WSL is a feature that allows Linux binaries to be run natively on Windows.

### DESKTOP EXPERIENCE VS SERVER CORE

[Windows Server Core](https://docs.microsoft.com/en-us/windows-server/administration/server-core/what-is-server-core) was first released with Windows Server 2008 as a minimalistic Server environment only containing key Server functionality. As a result, Server Core has lower management requirements, a smaller attack surface, and uses less disk space and memory than its Desktop Experience (GUI) counterpart.

### WINDOWS SECURITY

Due to the many built-in applications, features, and layers of settings, Windows systems can be easily misconfigured, thus opening them up to attack even if they are fully patched.

Microsoft has continued to add new features that can be used by systems administrators to harden systems and actively block and detect attempts at intrusion and misuse.

Windows follows certain security principles to control access and authentication within the system. These principles apply to various entities, such as users, networked computers, threads, and processes, which can be authorized for specific actions.

#### Security Identifier (SID)












