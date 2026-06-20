
## INTRODUCTION
### Linux Structure

Ens explica breument la historia i la filosofia radere de Linux. 

També ens fa un repàs dels components de conformen el sistema operatiu:
- Bootloader
- OS Kernel
- Daemons
- OS Shell
- Graphics Server
- Winodws Manager
- Utilities (aplicacions varies)

Després segueix amb l'arquitecture de Linux:
- Hardware
- Kernel
- Shell
- System Utility

Per últim ens ensenya la jerarquia d'arxius de Linux:

![[NEW_filesystem.png]]

### Linux Distribution

Veiem les diferents distribucions principals de Linux.
- [Ubuntu](https://ubuntu.com/)
- [Fedora](https://fedoraproject.org//)
- [CentOS](https://www.centos.org/)
- [Debian](https://www.debian.org/)
- [Red Hat Enterprise Linux](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux)

Ens explica amb més detall una de les distros més utilitzades: DEBIAN.

### Introduction to Shell

Breu introducció al concepte de shell a Linux. La shell més utilitzada és BASH, pero n’hi han altres com zsh, ksh, etc.

## THE SHELL
### Prompt Description - The Shell

```
<username>@<hostname><current working directory>$
```

La variable PS1 (Prompt String) controla com se veu la consola (color, lletra, etc).

Es pot modificar el prompt per a que a més de la informació per defecte també mostri allò que ens podria interessar. Per exemple, la IP de la victima, la data i hora i el estat d'execució de l'última comanda utilitzada. Aquesta personalització és especialment útil durant els pentestings perque t'ajuda en el procés de documentació de l'auditoria.

També és interessant veure un històrics de les comandes executades. Això ho podem trobar a l'arxiu .bash_history o utilitzant una eina com script.

A l'arxiu .bash_rc podem personalitzar variables i caràcters especials.

"[Bash-prompt-generator](https://bash-prompt-generator.org/)" i "[powerline](https://github.com/powerline/powerline)" son eines que serveixen per personalitzar la comand prompt.

### Getting Help

man, - - help, -h

Eines útils per a info sobre comandes:
- apropos
- [explainshell](https://explainshell.com/)

### System Infromation

- És important entendre l'estructura de Linux, incloent detalls del sistema, dels seus processos, configuracions de xarxa, configuracions d'usuaris, estructura de directoris, etc. A continuació tenim una llista d'eines essencials per recopilar aquesta informació:


| whoami   | Displays current username.                                                                                                         |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| id       | Returns users identity.                                                                                                            |
| hostname | Sets or prints the name of current host system.                                                                                    |
| uname    | Prints basic information about the operating system name and system hardware.                                                      |
| pwd      | Returns working directory name.                                                                                                    |
| ifconfig | The ifconfig utility is used to assign or to view an address to a network interface and/or configure network interface parameters. |
| ip       | Ip is a utility to show or manipulate routing, network devices, interfaces and tunnels.                                            |
| netstat  | Shows network status.                                                                                                              |
| ss       | Another utility to investigate sockets.                                                                                            |
| ps       | Another utility to investigate sockets.                                                                                            |
| who      | Displays who is logged in.                                                                                                         |
| env      | Prints environment or sets and executes command.                                                                                   |
| lsblk    | Lists block devices.                                                                                                               |
| lsusb    | Lists USB devices.                                                                                                                 |
| lsof     | Lists opened files.                                                                                                                |
| lspci    | Lists PCI devices.                                                                                                                 |
Exemples:

```
uname -r: Obtains Kernel Release version
```
## WORKFLOW
### Navigation

pwd, ls, cd

### Working with Files and Directories

Editors de consola més utilitzats: vim, nano

| COMANDA                            | EXPLICACIÓ                                   |
| ---------------------------------- | -------------------------------------------- |
| touch \<name>                      | Crea un fitxer.                              |
| mkdir \<name>                      | Crea un directori.                           |
| tree .                             | Mostra l'estructura de directoris i fitxers. |
| mv \<file/dir> \<renamed file/dir> | Rename a file/dir.                           |
### Editing Files

Editors de consola més utilitzats: vim, nano

Nano és més intuitiu i fàcil d'utilitzar i vim és més potent però no gaire intuitiu.

### Find Files and Directories


| COMANDA                     | EXPLICACIÓ                                                                                                                                |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------- |
| wich \<program_name>        | Ens permet determinar si un programa en específic està disponible al nostre sistema.                                                      |
| find \<location> \<options> | Eina molt potenta per buscar arxius o directoris. Ens permet filtrar els resultats en funció els opcions que li passem.                   |
| locate                      | També eina molt potenta per buscar arxius i directoris. No ens permet filtrar amb tantes opcions com find però té la sintaxis més simple. |

### File Descriptors and Redirections


El File Descriptor (FD) és un identificador únic de cad arxiu el qual és utilitzat pel sistema Linux per gestionar les operacions i conexions de Input / Output.

Per defecte, els tres primers File Descriptors a Linux son:
1. Data Stream for Input (STDIN - 0)
2. Data Stream for Output (STDOUT - 1)
3. Data Stream for Output that relates to an error ocurring (STDERR - 2)

Per redirigir l'output a un arxiu:
- Overwrite >
- Append >>
- output 1>
- error 2>

També cal destacar lo útil que son les canonades per redirigir outputs que faran de input.
- |


### Filter Contents

Let's talk about reading files directly from the command line, without needing to open a text editor.

There are two powerful tools for this:
- more
- less

Però avegades sol volem veure el principi o el final:
- Head
- Tail

També ens pot interessar ordenar l'output amb un determinat ordre:
- Sort

Linux també ens permet filtrar l'output per a que sol mostri allò que ens interessa.
- grep

Si volem treure basura de l'ouput.
- cut

Si volem transformar l'ouput.
- tr

Si volem formatejar l'output en format taula.
- Column

Extra:

- awk
- sed
- wc


### Regular Expressions

Les expressions regulars serveixen per buscar patrons dins del text com podries ser emails, numero de telefon, etc. 

Aquests patrons es poden personalitzar amb molt detall. Els patrons estan formats per metacaràcters que son els encarregats de determinar quin patró es vol buscar.

### Permission Management

Each user belongs to multiple groups, and being part of a group grants additional access rights, allowing users to eprform specific actions on files and directories.

Every file and directory has an owner (a user) and is associated with a group.


| COMANDA | EXPLICACIÓ                                  |
| ------- | ------------------------------------------- |
| chmod   | Canvia els permisos d'un arxiu o directori  |
| chown   | Canvia el propietori d'un arxiu o directori |
### SUID & SGID

Permet atribuir permisos temporals. Per més informació es pot visitar GTFObins.

## SYSTEM MANAGEMENT
### User Management

Una gestió efectiva dels usuaris és un aspecte fonamental de l'administració de sistemes Linux.


| COMANDA  | EXPLICACIÓ                                                     |
| -------- | -------------------------------------------------------------- |
| sudo     | Executa la comanda com si fossis un usuari different.          |
| su       | Serveix per canviar d'usuari dins la shell.                    |
| useradd  | Crea un usari nou o actualitza la informació d'un ja existent. |
| userdel  | Elimina un usuari i la seva informació.                        |
| addgroup | Afegeix un usuari a un grup.                                   |
| delgroup | Elimina un grup del sistema.                                   |
| passwd   | Canvia la contrasenya de l'usuari qui executa la comanda.      |

### Package Management

dpkg, apt, aptitude, snap, gem, pip, git

Profunditza en apt, git i dpkg.

### Service and Process Management
Services, also known as daemons, are fundamental components of a Linux system that run silently in the background "without direct user interaction".


- **System Services:** Aquests son serveis interns necessaris pel setup del sistema. Realitzem tasques essencials per al funcionament del sistema operatiu i hardware.
- **User-Installed Services:** Aquests serveis son afegits per l'usuari. Treballen en segon pla i afegeixen features o capabilities al sistema. Normalment els daemons s'identifiquen amb la lletra d. Les tasques que es realitzen en aquests serveis son:
	1. Start / Restart a service/process.
	2. Stop a service/process
	3. See what is/was happening with a service/process.
	4. Enable/Disable a service/process on boot.
	5. Find a service/process.

- Systemctl

| COMANDA                                   | EXPLICACIÓ                                         |
| ----------------------------------------- | -------------------------------------------------- |
| ```systemctl start/stop ssh```            | Iniciar/parar un servei                            |
| ```systemctl status ssh```                | Mostra l'estat del servei                          |
| ```systemctl enable ssh```                | Tell the system to run this service after startup. |
| ```systemctl list-units --type=service``` | Lliste tots els serveis que estan en execució.     |
| ```journalctl -u ssh.service```           | Mostra els logs de ssh.                            |

- Kill
S'utilitza per controlar procesos mitjançant l'enviament de senyals.

Les comandes que podem utilitzar son: kill, pkill, pgrep, killall
Les senyals més utilizades son:

|     | SENYAL  | EXPLICACIÓ                                                                                                  |
| --- | ------- | ----------------------------------------------------------------------------------------------------------- |
| 1   | SIGHUP  | This is sent to a process when the terminal that controls it is closed.                                     |
| 2   | SIGINT  | Sent when a user presses \[Ctrl] + C in the controlling terminal to interrupt a process.                    |
| 3   | SIGQUIT | Sent when a user presses \[Ctrl] + D to quit.                                                               |
| 9   | SIGKILL | Immediately kill a process with no clean-up operations.                                                     |
| 15  | SIGTERM | Program termination.                                                                                        |
| 19  | SIGTERM | Program termination.                                                                                        |
| 20  | SIGTSTP | Sent when a user presses \[Ctrl] + Z to request for a service to suspend. The user can handle it afterward. |

#### Background a Process

Avegades serà necessari possar un procés en segon pla o tornarlo a primer pla. Quan un procés es posa a segon pla, aquest es pausa. També és interessant fer que el procés s'executi al background amb bg.


| COMANDA  | EXPLICACIÓ                                                       |
| -------- | ---------------------------------------------------------------- |
| jobs     | Llista tots els procesos executant-se en segon pla.              |
| CTRL + Z | Atura i envia un procés al background.                           |
| bg       | Envia un procés al background sense aturar-lo.                   |
| fg \<id> | Per tornar un procés al frontground i poder interactuar amb ell. |

#### Execute Multiple Commands

Hi han tres possibilitats per executar varies comandes una rere l'altra.
- ;
- &&
- |

#### Task Scheduling

 Knowledge of how tasks are automated allows you to identify potential security risks, such as unauthorized cron jobs that execute harmful scripts or maintain persistent backdoors at scheduled intervals.
- Systemd
- Cron

## LINUX NETWORKING
### Network Services

While it is not feasible to cover every network service, we will focus on the most important ones.

### SSH

OpenSSH es pot configurar i personalitzar editant l'arxiu */etc/ssh/sshd_config*

| COMANDA                                  | EXPLICACIÓ      |
| ---------------------------------------- | --------------- |
| ```sudo apt install openssh-server -y``` | Install OpenSSH |
| ```systemctl status ssh```               | Server Status   |
| ```ssh user@10.129.17.122```             | Loggin in       |

### NFS

Network File System (NFS) és un protocol que ens permet guardar i gestionar arxius de manera remota com si estiguessin guardats localment al nostre sistema.

Podem configurar NFS editant /etc/exports.

| COMANDA                                     | EXPLICACIÓ    |
| ------------------------------------------- | ------------- |
| ```sudo apt install nfs-kernel-server -y``` | Install NFS   |
| ```systemctl status nfs-kernel-server```    | Server Status |
1. Create NFS Share
2. Mount NFS Share

#### Web Server

Per a configurar el servidor podem editar l'arxiu `/etc/apache2/apache2.conf`

| COMANDA                                                              | EXPLICACIÓ                            |
| -------------------------------------------------------------------- | ------------------------------------- |
| ```sudo apt install apache2 -y```                                    | Install apache web server             |
| ```python3 -m http.server --directory /home/username/target_files``` | Start a Python web server on TCP/8000 |
| ```python3 -m http.server 443```                                     | Start a Python web server on TCP/443  |


#### VPN

Per a configurar OpenVPN `/etc/openvpn/server.conf`

### Working with Web Services

Setting up a web server on a Linux operating system can be done in several ways, with popular options including Nginx, IIS, and Apache. Among these, Apache is one of the most widely used web servers.


| COMANDA                            | EXPLICACIÓ               |
| ---------------------------------- | ------------------------ |
| ```sudo apt install apache2 -y```  | Install apache.          |
| ```sudo systemctl start apache2``` | Iniciem el servidor web. |
| ```curl```                         |                          |
| ```wget```                         |                          |
Per modificar el port en el qual corre apache ho farem modificant l'arxiu de configuració `/etc/apache2/ports.conf`

### Backup and Restore

Linux systems provide a range of powerful tools for backing up and restoring data, designed to be both efficient and secure.

- Rsync
- Deja Dup (graphical)
- Duplicity

| COMANDA                                                                           | EXPLICACIÓ                                    |
| --------------------------------------------------------------------------------- | --------------------------------------------- |
| ```sudo apt install rsync -y```                                                   | Install rsync                                 |
| ```rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory``` | Backup a local Directory to our Backup-Server |
| ```rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory```   | Restore our backup                            |

L'eina rsync permet fer tant backups complerts com incrementals.

Per automatitzar els backups ho tenim que fer mitjançant cron i una clau pública de ssh.

### File System Management

Linux is a versatile operating system that supports many different file systems, including ext2, ext3, ext4, XFS, Btrfs, and NTFS, among others. Each of these file systems has unique features and is suited to specific use cases.

In Linux, files can be stored in one of several key types:

- Regular files
- Directories
- Symbolic links

#### Disks & Drives
Disk management on Linux involves managing physical storage devices, including hard drives, solid-state drives, and removable storage devices. The main tool for disk management on Linux is the `fdisk`.

#### Mounting
Each logical partition or storage drive must be assigned to a specific directory in the file system. This process is known as `mounting`

Once a drive is mounted to a directory (also called a mount point), it can be accessed and used like any other directory on the system.


| COMANDA                             | EXPLICACIÓ          |
| ----------------------------------- | ------------------- |
| ```mount```                         | List mounted drives |
| ```sudo mount /dev/sdb1 /mnt/usb``` | Mount a USB drive   |
| ```sudo unmount /mnt/usb```         |                     |


### Containerization


Containerization is the process of packaging and running applications in isolated environments, typically referred to as containers.

Technologies like Docker, Docker Compose, and Linux Containers (LXC) make containerization possible, primarily in Linux-based systems.

Containers are highly configurable, allowing users to tailor them to their specific needs, and their lightweight nature makes it easy to run multiple containers simultaneously on the same host system.

### Network Configuration

One of the primary tasks in network configuration is managing network interfaces. This involves assigning IP addresses, configuring network devices such as routers and switches, and setting up various network protocols. TCP/IP, DNS, DHCP, FTP.

#### Configuring network interfaces



### Remote Desktop Protocols in Linux

Remote desktop protocols provide graphical remote access to a system.

An administrator connects to the remote system using the appropriate protocol depending on the operating system they are managing.

- Remote Desktop Protocol (RDP)
- Virtual Network Computing (VNC)


## LINUX HARDENING
### Linux Security

Linux systems are also less prone to viruses that affect Windows operating systems and do not present as large an attack surface as Active Directory domain-joined hosts. Regardless, it is essential to have certain fundamentals in place to secure any Linux system.

One of the Linux operating systems' most important security measures is keeping the OS and installed packages up to date.

```apt update && apt dist-upgrade```

| COMANDA        | EXPLICACIÓ                                                    |
| -------------- | ------------------------------------------------------------- |
| ```iptables``` | Restrict traffic into/out of the host.                        |
| ```fail2ban``` | Counts the number of failed login attempts and blocks the ip. |
An option for further locking down Linux systems is `Security-Enhanced Linux` (`SELinux`) or `AppArmor`. This is a kernel security module that can be used for security access control policies.

In addition, some security settings should be made, such as:

- Removing or disabling all unnecessary services and software
- Removing all services that rely on unencrypted authentication mechanisms
- Ensure NTP is enabled and Syslog is running
- Ensure that each user has its own account
- Enforce the use of strong passwords
- Set up password aging and restrict the use of previous passwords
- Locking user accounts after login failures
- Disable all unwanted SUID/SGID binaries

### Firewall Setup
The primary goal of firewalls is to provide a security mechanism for controlling and monitoring network traffic between different network segments, such as internal and external networks or different network zones.

 iptables was designed to be highly customizable and could be used to create complex firewall rulesets that could protect against various security threats such as denial-of-service (DoS) attacks, port scans, and network intrusion attempts.

#### Iptables
The iptables utility provides a flexible set of rules for filtering network traffic based on various criteria such as source and destination IP addresses, port numbers, protocols, and more.


## SYSTEM LOGS AND MONITORING
### System Logs
System logs on Linux are a set of files that contain information about the system and the activities taking place on it. These logs are important for monitoring and troubleshooting the system, as they can provide insights into system behavior, application activity, and security events.

There are several different types of system logs on Linux, including:

- Kernel Logs --- ```/var/log/kern.log```
- System Logs --- `var/log/syslog`
- Authentication Logs --- `/var/log/auth.log`
- Application Logs 
	- `/var/log/apache2/error.log`
	- `/var/log/mysql/error.log`
	- etc
- Security Logs
	- `/var/log/fail2ban.log`
	- `/var/log/ufw.log`
	- 


