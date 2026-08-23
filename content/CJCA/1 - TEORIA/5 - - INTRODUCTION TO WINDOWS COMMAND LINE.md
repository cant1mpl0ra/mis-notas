

## INTRODUCTION

The built-in command shell CMD.exe and PowerShell are two implementations included in all Windows hosts. These tools provide direct access to the operating system, automate routine tasks, and provide the user with granular control of any aspect of the computer and installed applications.

| PowerShell                                                                 | CMD                                                   |
| -------------------------------------------------------------------------- | ----------------------------------------------------- |
| Introduced in 2006                                                         | Introduced in 1981                                    |
| Can run both batch commands and PowerShell cmdlets                         | Can only run batch commands                           |
| Supports the use of command aliases                                        | Does not support command aliases                      |
| Cmdlet output can be passed to other cmdlets                               | Command output cannot be passed to other commands     |
| All output is in the form of an object                                     | Output of commands is text                            |
| Able to execute a sequence of cmdlets in a script                          | A command must finish before the next command can run |
| Has an Integrated Scripting Environment (ISE)                              | Does not have an ISE                                  |
| Can access programming libraries because it is built on the .NET framework | Cannot access these libraries                         |
| Can be run on Linux systems                                                | Can only be run on Windows systems                    |
## CMD

### Command Prompt Basics

It allows users to input commands that are directly interpreted and then executed by the operating system.

Remote access protocols: SSH, PsExec, WinRM, RDP.

Comandes explicades: dir

### Getting Help


The Command Prompt has a built-in `help` function that can provide us with detailed information about the available commands on our system and how to utilize those functions.

Hi han comandes que help no funcione i aleshores has d'utilitzar /?

[ss64](https://ss64.com/nt/) Is a handy quick reference for anything command-line related, including cmd, PowerShell, Bash, and more.

Comandes explicades: cls, doskey

`doskey history` --> Mostra l'historial de comandes

### System Navigation

Absoulte vs Relative PATH

Comandes explicades: tree

We can utilize the `/F` parameter with the tree command to see a listing of each file and the directories along with the directory tree of the path.
#### Interesting Directories

Below is a table of common directories that an attacker can abuse to drop files to disk, perform reconnaissance, and help facilitate attack surface mapping on a target host.

| Name:               | Location:                            | Description:                                                                                                                                                                                                                                                                     |
| ------------------- | ------------------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| %SYSTEMROOT%\Temp   | `C:\Windows\Temp`                    | Global directory containing temporary system files accessible to all users on the system. All users, regardless of authority, are provided full read, write, and execute permissions in this directory. Useful for dropping files as a low-privilege user on the system.         |
| %TEMP%              | `C:\Users\<user>\AppData\Local\Temp` | Local directory containing a user's temporary files accessible only to the user account that it is attached to. Provides full ownership to the user that owns this folder. Useful when the attacker gains control of a local/domain joined user account.                         |
| %PUBLIC%            | `C:\Users\Public`                    | Publicly accessible directory allowing any interactive logon account full access to read, write, modify, execute, etc., files and subfolders within the directory. Alternative to the global Windows Temp Directory as it's less likely to be monitored for suspicious activity. |
| %ProgramFiles%      | `C:\Program Files`                   | folder containing all 64-bit applications installed on the system. Useful for seeing what kind of applications are installed on the target system.                                                                                                                               |
| %ProgramFiles(x86)% | `C:\Program Files (x86)`             | Folder containing all 32-bit applications installed on the system. Useful for seeing what kind of applications are installed on the target system.                                                                                                                               |
### Working with Directories and Files - CMD

Comandes explicades: mkdir, rd /s, rmdir, move, xcopy, robocopy, more, ren, 
#### Robocopy Basic

`robocopy C:\Users\htb\Desktop C:\Users\htb\Documents\`

 The `/MIR` switch will mirror the destination directory to the source.

#### Interesting Commands

| COMANDA                                                            | DESCRIPCIÓ                              |
| ------------------------------------------------------------------ | --------------------------------------- |
| `echo Check out this text > demo.txt`                              | Echo to create and append files.        |
| `ren demo.txt superdemo.txt`                                       | Rename a file.                          |
| `ipconfig /all > details.txt`                                      | Output to a file.                       |
| `echo hello >> test.txt`                                           | Append to a file.                       |
| `find /i "see" < test.txt`                                         | Pass in a Text File to a Command.       |
| `ipconfig /all \| find /i "IPV4"`                                  | Pipe output between commands.           |
| `ping 8.8.8.8 & type test.txt`                                     | Run A then B.                           |
| `erase file-3 file-5`                                              | Remove a list of files.                 |
| `dir /A:R`                                                         | View files with the read-only attribute |
| `del /A:R *`                                                       | Deleta a read-only file                 |
| `dir /A:H`                                                         | Viewing hidden files                    |
| `move C:\Users\student\Desktop\bio.txt C:\Users\student\Downloads` | Move a file                             |

### Gathering System Information

It is a crucial step in providing a good foundation for getting to know our environment.

The goal of `host enumeration` is to provide an overall picture of the target host, its environment, and how it interacts with other systems across the network.

The types of information that we would be looking for can be broken down into the following categories:

![[InformationTypesChart_Updated (1).png]]

|Type|Description|
|---|---|
|`General System Information`|Contains information about the overall target system. Target system information includes but is not limited to the `hostname` of the machine, OS-specific details (`name`, `version`, `configuration`, etc.), and `installed hotfixes/patches` for the system.|
|`Networking Information`|Contains networking and connection information for the target system and system(s) to which the target is connected over the network. Examples of networking information include but are not limited to the following: `host IP address`, `available network interfaces`, `accessible subnets`, `DNS server(s)`, `known hosts`, and `network resources`.|
|`Basic Domain Information`|Contains Active Directory information regarding the domain to which the target system is connected.|
|`User Information`|Contains information regarding local users and groups on the target system. This can typically be expanded to contain anything accessible to these accounts, such as `environment variables`, `currently running tasks`, `scheduled tasks`, and `known services`.|
Our `goal` with `host enumeration` here is to use the information gained from the target to provide us with a starting point and guide for how we wish to attack the system.

Preguntes que ens tenim que respondre durant la enumeració:
- What user account do we have access to?
- What groups does our user belong to?
- What current working set of privileges does our user have access to?
- What resources can our user access over the network?
- What tasks and services are running under our user account?

#### How do we get this information?
CMD provides a one-stop shop for information via the `systeminfo` command. It is excellent for finding relevant information about the host, such as hostname, IP address(es), if it belongs to a domain, what hotfixes have been installed, and much more.

Running one command is always better than running two or three just to get the same information.


| COMANDA          | DESCRIPCIÓ                                                                                 |
| ---------------- | ------------------------------------------------------------------------------------------ |
| `arp /a`         | Find additional hosts in the network                                                       |
| `whoami`         | Shows the user, group, and privilege information for the user that is currently logged in. |
| whoami /priv     | Checking out our privileges                                                                |
| whoami /groups   | Investigating groups                                                                       |
| whoami /all      | Gathers all the information at once                                                        |
| `net user`       | Displays a list of all users on a host,                                                    |
| `net group`      | Displays groups from a domain server                                                       |
| `net localgroup` | Can be run against any host to show us the groups it contains.                             |
| `net share`      | Displays info about shared resources on the host.                                          |
| `net view`       | Displays to us any shared resources the host you are issuing the command against knows of. |
### Finding Files and Directories

#### Where

`where calc.exe`

Si el programa que volem ubicar està en una carpeta que no tenim al PATH, aleshores tindrem que realitzar una búsqueda recursiva indicant-li la carpeta on volem buscar.

`where /R C:\Users\students bio.txt`

Podem utilitzar wildcards en la búsqueda.

`where /R C:\Users\student\ *.csv`

#### Find
Find is used to search for text strings or their absence within a file or files. You can also use `find` against the console's output or another command.

`find "password" "C:\Users\student\not-passwords.txt"`
#### Compare
`Comp` will check each byte within two files looking for differences and then displays where they start. By default, the differences are shown in a decimal format. We can use the `/A` modifier if we want to see the differences in ASCII format. The `/L` modifier can also provide us with the line numbers.

`comp .\file-1.md .\file-2.md`

![[Pasted image 20260625201537.png]]

#### FC
When FC performs its inspection, it is case-sensitive and cares more than just a byte-for-byte comparison. Below we will use a few files with many more characters and strings to test its functionality. We will perform a basic check and have it print the line numbers and the ASCII comparison using the `/N` modifier.

### Environment Variables

Environment variables are settings that are often applied globally to our hosts.

Environment variables can be accessed by most users and applications on the host and are used to run scripts and speed up how applications function and reference data.

#### Variable Scope

Gobal Variable
![[Pasted image 20260627152551.png]]

Local Variable
![[Pasted image 20260627152611.png]]

#### Managing Environment Variables

We have two methods available to us to do so. We can either use `set` or `setx` to perform our intended actions. Both [set](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/set_1) and [setx](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/setx) are command line utilities that allow us to display, set, and remove environment variables. The difference lies in how they achieve those goals.

The `set` utility only manipulates environment variables in the current command line session. This means that once we close our current session, any additions, removals, or changes will not be reflected the next time we open a command prompt.

We can use `setx` to make the appropriate changes to the registry, which will exist upon restart of our current command prompt session.

To remove variables, we cannot directly delete them like we would a file or directory; instead, we must clear their values by setting them equal to nothing.

![[Pasted image 20260627154654.png]]

#### Important Environment Variables
There are some crucial variables we should be aware of when performing enumeration on a host's environment. As an attacker, this can provide us with a wealth of information about the current system and the user account accessing it.

|Variable Name|Description|
|---|---|
|`%PATH%`|Specifies a set of directories(locations) where executable programs are located.|
|`%OS%`|The current operating system on the user's workstation.|
|`%SYSTEMROOT%`|Expands to `C:\Windows`. A system-defined read-only variable containing the Windows system folder. Anything Windows considers important to its core functionality is found here, including important data, core system binaries, and configuration files.|
|`%LOGONSERVER%`|Provides us with the login server for the currently active user followed by the machine's hostname. We can use this information to know if a machine is joined to a domain or workgroup.|
|`%USERPROFILE%`|Provides us with the location of the currently active user's home directory. Expands to `C:\Users\{username}`.|
|`%ProgramFiles%`|Equivalent of `C:\Program Files`. This location is where all the programs are installed on an `x64` based system.|
|`%ProgramFiles(x86)%`|Equivalent of `C:\Program Files (x86)`. This location is where all 32-bit programs running under `WOW64` are installed. Note that this variable is only accessible on a 64-bit host. It can be used to indicate what kind of host we are interacting with. (`x86` vs. `x64` architecture)|
### Managing Services

We will look at the usage of `sc`, the Windows command line service controller utility. From the perspective of an attacker we wanna:

- Determine what services are running.
- Attempt to disable antivirus.
- Modify existing services on a system.

#### Service Controller
[SC](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/cc754599\(v=ws.11\)) is a Windows executable utility that allows us to query, modify, and manage host services locally and over the network.

We have other tools, like Windows Management Instrumentation (`WMIC`) and `Tasklist` that can also query and manage services for local and remote hosts. But in this section we will focus on sc.

#### Query Services 
Being able to `query` services for information such as the `process state`, `process id` (`pid`), and `service type` is a valuable tool to have in our arsenal as an attacker. We can query all active services like this:

![[Pasted image 20260628165336.png]]

#### Stopping and Starting Services

Hi han serveis (com el de windows defender) que no podem aturar amb la compta Administrador i necessitem la compta amb més privilegis coneguda com SYSTEM.

Ara bé hi han serveis com el Print Spooler service els quals podem aturar amb privilegis d'administrador.

![[Pasted image 20260628165904.png]]

![[Pasted image 20260628170018.png]]

També podem configurar un servei amb el parametre config de sc. Els canvis que li fem a la configuració quedaran guardats de forma persistent al registre.

![[Pasted image 20260628170542.png]]

#### Other routes to query services
[Tasklist](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/tasklist) is a command line tool that gives us a list of currently running processes on a local or remote host. However, we can utilize the `/svc` parameter to provide a list of services running under each process on the system.

![[Pasted image 20260628170744.png]]

As we can see, we have a full listing of processes that are currently running on the system, their respective `PID`, and what service(s) are hosted under each process

[Net start](https://ss64.com/nt/net-service.html) is a very simple command that will allow us to quickly list all of the current running services on a system. In addition to `net start`, there is also `net stop`, `net pause`, and `net continue`.

Using `net start` without specifying a `service` will list all of the active services on the system.

![[Pasted image 20260628171009.png]]

Last but not least, we have [WMIC](https://ss64.com/nt/wmic.html). The Windows Management Instrumentation Command (`WMIC`) allows us to retrieve a vast range of information from our local host or host(s) across the network.

To list all services existing on our system and information on them, we can issue the following command: `wmic service list brief` .


### Working With Scheduled Tasks

The scheduler will monitor the host for a specific set of conditions called triggers and execute the task once the conditions are met.

#### Query Syntax

|**Action**|**Parameter**|**Description**|
|---|---|---|
|`Query`||Performs a local or remote host search to determine what scheduled tasks exist. Due to permissions, not all tasks may be seen by a normal user.|
||/fo|Sets formatting options. We can specify to show results in the `Table, List, or CSV` output.|
||/v|Sets verbosity to on, displaying the `advanced properties` set in displayed tasks when used with the List or CSV output parameter.|
||/nh|Simplifies the output using the Table or CSV output format. This switch `removes` the `column headers`.|
||/s|Sets the DNS name or IP address of the host we want to connect to. `Localhost` is the `default` specified. If `/s` is utilized, we are connecting to a remote host and must format it as "\\host".|
||/u|This switch will tell schtasks to run the following command with the `permission set` of the `user` specified.|
||/p|Sets the `password` in use for command execution when we specify a user to run the task. Users must be members of the Administrator's group on the host (or in the domain). The `u` and `p` values are only valid when used with the `s` parameter.|
We can view the tasks that already exist on our host by utilizing the `schtasks` command like so:

![[Pasted image 20260628171833.png]]

#### Create Syntax
|**Action**|**Parameter**|**Description**|
|---|---|---|
|`Create`||Schedules a task to run.|
||/sc|Sets the schedule type. It can be by the minute, hourly, weekly, and much more. Be sure to check the options parameters.|
||/tn|Sets the name for the task we are building. Each task must have a unique name.|
||/tr|Sets the trigger and task that should be run. This can be an executable, script, or batch file.|
||/s|Specify the host to run on, much like in Query.|
||/u|Specifies the local user or domain user to utilize|
||/p|Sets the Password of the user-specified.|
||/mo|Allows us to set a modifier to run within our set schedule. For example, every 5 hours every other day.|
||/rl|Allows us to limit the privileges of the task. Options here are `limited` access and `Highest`. Limited is the default value.|
||/z|Will set the task to be deleted after completion of its actions.|

Creating a new scheduled task is pretty straightforward. At a minimum, we must specify the following:

- `/create` : to tell it what we are doing
- `/sc` : we must set a schedule
- `/tn` : we must set the name
- `/tr` : we must give it an action to take

![[Pasted image 20260628172040.png]]

#### Change Syntax
|**Action**|**Parameter**|**Description**|
|---|---|---|
|`Change`||Allows for modifying existing scheduled tasks.|
||/tn|Designates the task to change|
||/tr|Modifies the program or action that the task runs.|
||/ENABLE|Change the state of the task to Enabled.|
||/DISABLE|Change the state of the task to Disabled.|
![[Pasted image 20260628180503.png]]

#### Delete Syntax
|**Action**|**Parameter**|**Description**|
|---|---|---|
|`Delete`||Remove a task from the schedule|
||/tn|Identifies the task to delete.|
||/s|Specifies the name or IP address to delete the task from.|
||/u|Specifies the user to run the task as.|
||/p|Specifies the password to run the task as.|
||/f|Stops the confirmation warning.|
![[Pasted image 20260628180543.png]]

## POWERSHELL
### CMD vs PowerShell

[PowerShell](https://learn.microsoft.com/en-us/powershell/scripting/overview?view=powershell-7.2) is the modern successor to CMD. 

|**Feature**|**CMD**|**PowerShell**|
|---|---|---|
|Language|Batch and basic CMD commands only.|PowerShell can interpret Batch, CMD, PS cmdlets, and aliases.|
|Command utilization|The output from one command cannot be passed into another directly as a structured object, due to the limitation of handling the text output.|The output from one command can be passed into another directly as a structured object resulting in more sophisticated commands.|
|Command Output|Text only.|PowerShell outputs in object formatting.|
|Parallel Execution|CMD must finish one command before running another.|PowerShell can multi-thread commands to run in parallel.|

#### Why choose PoserShell over cmd.exe?
PowerShell can provide us with much more capability than `CMD`. It is `expandable`, built for `automation` and scripting, has a much more robust security implementation, and can handle many different tasks that CMD simply cannot.

| COMANDA                    | EXPLICACIÓ                                                |
| -------------------------- | --------------------------------------------------------- |
| Get-ChildItem              | List the directory.                                       |
| Set-Location               | Move to a new directory.                                  |
| Get-Content                | Display contents of a file.                               |
| Get-Command -verb get      | Serveix per buscar comandes especifiques en base al verb. |
| Get-Command -noun windows* | Serveix per buscar comandes específiques en base el nom.  |
| Get-History                | Mostra l'historial de comandes                            |
| Get-Alias                  | Mostra els alias declarats.                               |
#### Helpful Aliases
|**Alias**|**Description**|
|---|---|
|`pwd`|gl can also be used. This alias can be used in place of Get-Location.|
|`ls`|dir and gci can also be used in place of ls. This is an alias for Get-ChildItem.|
|`cd`|sl and chdir can be used in place of cd. This is an alias for Set-Location.|
|`cat`|type and gc can also be used. This is an alias for Get-Content.|
|`clear`|Can be used in place of Clear-Host.|
|`curl`|Curl is an alias for Invoke-WebRequest, which can be used to download files. wget can also be used.|
|`fl and ft`|These aliases can be used to format output into list and table outputs.|
|`man`|Can be used in place of help.|

### All About Cmdlets and Modules
#### Cmdlets
A [cmdlet](https://docs.microsoft.com/en-us/powershell/scripting/lang-spec/chapter-13?view=powershell-7.2) as defined by Microsoft is:

"`a single-feature command that manipulates objects in PowerShell.`"

Cmdlets follow a Verb-Noun structure which often makes it easier for us to understand what any given cmdlet does.

#### PowerShell Modules
A [PowerShell module](https://docs.microsoft.com/en-us/powershell/scripting/developer/module/understanding-a-windows-powershell-module?view=powershell-7.2) is structured PowerShell code that is made easy to use & share. A module can be made up of the following:
- Cmdlets
- Script files
- Functions
- Assemblies
- Related resources (manifests and help files)

For example, `PowerView.ps1` is part of a collection of PowerShell modules organized in a project called [PowerSploit](https://github.com/PowerShellMafia/PowerSploit) created by the [PowerShellMafia](https://github.com/PowerShellMafia/PowerSploit) to provide penetration testers with many valuable tools to use when testing Windows Domain/Active Directory environments.

#### Using PowerShell Modules

| COMANDA                  | FUNCIÓ                                                                                    |
| ------------------------ | ----------------------------------------------------------------------------------------- |
| Get-Module               | What modules are already loaded.                                                          |
| Get-Module -ListAvailabe | This modifier will show us all modules we have installed but not loaded into our session. |
| Import-Module            | Allow us to add a module to the current PowerShell session.                               |
#### Execution policy
 [PowerShell's execution policy](https://docs.microsoft.com/en-us/powersh ell/module/microsoft.powershell.core/about/about_execution_policies?view=powershell-7.2) is designed to give IT admins a tool to set parameters and safeguards for themselves.

As penetration testers, we may run into times when we need to be creative about how we bypass the Execution Policy on a host. This [blog post](https://www.netspi.com/blog/technical/network-penetration-testing/15-ways-to-bypass-the-powershell-execution-policy/) has some creative ways that we have used on real-world engagements with great success.

- Checking execution policy state - - - `Get-ExecutionPolicy`
- Setting execution policy - - - Set-ExecutionPolicy undefined

#### Tools to be aware of
Below we will quickly list a few PowerShell modules and projects we, as penetration testers and sysadmins, should be aware of.

- [AdminToolbox](https://www.powershellgallery.com/packages/AdminToolbox/11.0.8): AdminToolbox is a collection of helpful modules that allow system administrators to perform any number of actions dealing with things like Active Directory, Exchange, Network management, file and storage issues, and more.
- [ActiveDirectory](https://learn.microsoft.com/en-us/powershell/module/activedirectory/?view=windowsserver2022-ps): This module is a collection of local and remote administration tools for all things Active Directory. We can manage users, groups, permissions, and much more with it.
- [Empire / Situational Awareness](https://github.com/BC-SECURITY/Empire/tree/master/empire/server/data/module_source/situational_awareness): Is a collection of PowerShell modules and scripts that can provide us with situational awareness on a host and the domain they are apart of. This project is being maintained by [BC Security](https://github.com/BC-SECURITY) as a part of their Empire Framework.
- [Inveigh](https://github.com/Kevin-Robertson/Inveigh): Inveigh is a tool built to perform network spoofing and Man-in-the-middle attacks.
- [BloodHound / SharpHound](https://github.com/BloodHoundAD/BloodHound/tree/master/Collectors): Bloodhound/Sharphound allows us to visually map out an Active Directory Environment using graphical analysis tools and data collectors written in C# and PowerShell.

### User and Group Management

As a system administrator, user and group management is a key skill as our users are often our main asset to manage and, usually, an organization's largest attack vector.

#### User accounts
When thinking about accounts, we typically run into four different types:
- Service Accounts
- Built-in accounts
- Local users
- Domain users

#### Default local user accounts
Several accounts are created in every instance of Windows as the OS is installed to help with host management and basic usage.

|**Account**|**Description**|
|---|---|
|`Administrator`|This account is used to accomplish administrative tasks on the local host.|
|`Default Account`|The default account is used by the system for running multi-user auth apps like the Xbox utility.|
|`Guest Account`|This account is a limited rights account that allows users without a normal user account to access the host. It is disabled by default and should stay that way.|
|`WDAGUtility Account`|This account is in place for the Defender Application Guard, which can sandbox application sessions.|
#### Local vs Domain joined users
`Domain` users differ from `local` users in that they are granted rights from the domain to access resources such as file servers, printers, intranet hosts, and other objects based on user and group membership. Domain user accounts can log in to any host in the domain, while the local user only has permission to access the specific host they were created on.

#### User groups
Groups are a way to sort user accounts logically and, in doing so, provide granular permissions and access to resources without having to manage each user manually.

#### Adding/Removing/Editing user accounts & groups

| COMMAND                                                                            | DESCRIPTION                                              |
| ---------------------------------------------------------------------------------- | -------------------------------------------------------- |
| Get-LocalGroup                                                                     | Mostra els grups que existeixen en local en aquell host. |
| Get-LocalUser                                                                      | Mostra el usuaris que existeixen al host en local.       |
| New-LocalUser                                                                      | Crea un usuari local.                                    |
| Set-LocalUser                                                                      | Modifica les propietats d'un usuari.                     |
| `Set-LocalUser -Name "JLawrence" -Password $Password -Description "CEO EagleFang"` | Moficia el nom i la contrasenya.                         |
| `Add-LocalGroupMember -Group "Remote Desktop Users" -Member "JLawrence"`           | Afegeix un usuari a un grup.                             |

#### Managing domain users and groups
One requirement is to have the optional feature `Remote System Administration Tools` installed.

![[Pasted image 20260628212017.png]]

The above command will install all RSAT features. But if we wanna stay lightweight we can use:

`Rsat.ActiveDirectory.DS-LDS.Tools~~~~0.0.1.0`

#### Comandes

| COMMAND                                                                                                                                                                                                                                | DESCRIPTION                                                         |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `Get-ADUser -Filter *`                                                                                                                                                                                                                 | Grab all users within Active Directory                              |
| `Get-ADUser -Filter {EmailAddress -like '*greenhorn.corp'}`                                                                                                                                                                            | Retorne aqells usuaris que tingin el email acabat en greenhorn.corp |
| `New-ADUser -Name "MTanaka" -Surname "Tanaka" -GivenName "Mori" -Office "Security" -OtherAttributes @{'title'="Sensei";'mail'="MTanaka@greenhorn.corp"} -Accountpassword (Read-Host -AsSecureString "AccountPassword") -Enabled $true` | Afegeix un usuari al domini amb propietats                          |
| `Set-ADUser -Identity MTanaka -Description " Sensei to Security Analyst's Rocky, Colt, and Tum-Tum"`                                                                                                                                   | Canvia l'atribut descripció d'un usuari.                            |
#### Why is enumerating users and groups important?

We will often see users misconfigured. They may be given excessive permissions, added to unnecessary groups, or have weak/no passwords set.

Groups can be equally as valuable. Often groups will have nested membership, allowing users to gain privileges they may not need.

These misconfigurations can be easily found and visualized with Tools like [Bloodhound](https://github.com/BloodHoundAD/BloodHound). For a detailed look at enumerating Users and Groups, check out the Windows Privilege Escalation module.

### Working with Files and Directories - Powershell































































