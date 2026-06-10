## A) INTRODUCTION

#### A.1 Introduction to Digital Forensics

-> Digital Forensics és una branca especialitzada de la ciberseguretat que implica la recollida, preservació, anàlisis i presentació d'evidències digitals per investigar incidents cibernètics, activitats delictives i infraccions de seguretat.

##### KEY CONCEPTS

- Electronic evidence -> files, emails, logs, databases, network traffic, ...
- Preservation of evidence -> Garantir la integritat i l'autenticitat de l'evidència digital és crucial.
- Forensics process -> Identification, collection, examination, analysis, presentation.
- Types of cases -> Cybercrime, intellectual property, data breaches, ...

-> Security Operations Center (SOC) is the frontline defense against cyber threats. But, what happens when a breach occurs, or when an anomaly is detected? That's where digital forensics comes into play.

#### A.2 Windows Forensics Overview

-> In this section, we will provide a concise overview of the key Windows artifacts and forensics procedures.

##### NTFS (New Technology File System)

-> Default and most widely used file system in modern Windows operating systems and their server counterparts. The key forensics artifacts are:

1) File Metadata -> creation time, modification time, access time and attribute information.
2) Master File Table (MFT) Entries -> Examining MFT entries provides insights into file names, sizes, timestamps, and data storage locations.
3) File Slack and Unallocated Space -> File slack refers to the unused portion of a cluster that may contain data from a previous file. Digital forensics tools can help recover and analyze data from these areas.
4) File Signatures -> File headers and signatures can be usefull in identifying file types even when file extensions have been changed or obscured.
5) UpdateSequenceNumber (USN) Journal -> Forensic investigators can analyze the USN Journal to track file modifications, deletions and renames.
6) Windows shortcut file(LNK Files) -> These files can indicate which programs have been run on the system and when they were last executed.
7) Prefetch Files -> Improve the start up performance of applications. These files can indicate which programs have been run on the system and when they were executed.
8) Registry Hives -> Malicious activities or unauthorized changes can leave traces in the registry, which forensic investigators analyze to understand system modifications.
9) Shellbags -> Analyzing shellbags can reveal user navigation patterns and potentially identify accessed folders.
10) Thumbnail cache -> Store miniature previous of images and documents. These caches can reveal files that were recently viewed, even if the original files have been deleted.
11) Recycle bin
12) Alternate Data Streams(ADS)
13) Volume Shadow Copies -> NTFS supports Volume Shadow Copies, which are snapshots of the file system at different points in time.
14) Security Descriptors and ACLs

##### EXECUTION ARTIFACTS

-> Windows execution artifacts refer to the traces and evidence left behind on a Windows OS when programs and processes are executed. Some examples are:

- Prefetch Files -> Analyzing prefetch files can reveal a history of executed programs and the order in which they were run.
- Schimcache -> Schimcache can help investigators identify recently executed programs and their associated files.
- Amcache
- UserAssist
- Run MRU Lists
- Jump Lists
- LNK Files
- Recent items
- Windows Event Logs

![[Pasted image 20240511190805.png]]

##### WINDOWS PERSISTENCE ARTIFACTS
-> These persistence methods exploit various system components, such as registry key, startup processes, scheduled tasks and services, allowing to mantain access and control even after initial intrusion.
- Registry -> Acts as a crucial database, storing critical system settings for the Windows OS. Therefore, it's essential to routinely inspect Registry autorun keys.
(exemple)
- Scheduled tasts (schtasks) -> C:\Windows\System32\Tasks
- Services -> HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services

##### WEB BROWSER FORENSICS

-> It's a discipline centered on analyzing remants left by web browsers. Some of the pivotal browser forensic artifacts include:

- Browsing history
- Cookies
- Cache
- Bookmarks/Favorites
- Download History
- Autofill Data
- Search History
- Session Data
- Typed URLs
- Forma Data
- Passwords
- web Storage
- Favicons
- Tab Recovery Data
- Extensions and Add-ons

##### System Resource Usage Monitor (SRUM)

-> It's a feature introduced in Windows 8 and subsequent versions. SRUM meticulously tracks resource utilization and applications usage patterns. the data is housed in the C:\Windows\System32\sru\sru.dat file. The key facets of SRUM forensics encompass:
- Application Profiling -> SRUM information is crucial for understanding the software landscape on a system.
- ResourceConsumption -> Poden detectar patrons inusuals en el consum dels recursos gràcies a la data que proporciona SRUM sobre el CPU time, network usage, and memory consumption for each application and process.
- Timeline Reconstruction -> By analyzing SRUM data, digital forensics experts can create timelines of applications and process execution, resource usage, and system activities.
- User and System Context
- Malware analysis and Detection
- Incident Response.

#### Evidence Acquisition Techniques and Tools

-> Is the collection of digital artifacts and data from various sources to preserve potential evidence for analysis. This process requires specialized tools and techniques to ensure the integrity, authenticity, and admissibility of the collected evidence. Main techniques are:

- Forensic Imaging
- Extracting Host-based Evidence and Rapid Triage
- Extracting Network Evidence

#####  FORENSIC IMAGING
-> Process taht involves creating an exact, bit-by-bit copy of digital storage media, such as hard drives, solid-state drives, USB drives, and memory cards.

-> Some tools and solutions are:

- FTKImager
- AFF4Imager
- DD and DCFLDD
- Visualization tools


- Example 1 -> Forensic Imaging with FTK Imager
- Example 2 -> Mounting a Disk Image with Arsenal Image Mounter

##### EXTRACTING HOST-BASED EVIDENCE and RAPID TRIAGE 

1) Host-based Evidence 

	-> Malware often leaves traces within system memory, and losing this evidence can hinder an analyst's investigation. To capture memory, tools like FTK Imager are commonly employed. Some other solutions are: WinPmem, DumpIt, MemDump, Belkafost RAM capturer, Magnet RAM, LiME.

- Example 1 -> Acquiring memory with WinPmem
- Example 2 -> Acquiring VM Memory

3) Rapid Triage

	-> The goal is to centralized high-value data, streamlining its indexing and analysis. By centralizing this data, analysts can more effectively deploy tools and techniques, honing in on systems with the most evidentiary value.
	
	-> KAPE (Kroll artifact Parser and Extractor) is one of the best, if not the best, rapid artifact parsing and extracting solution.
	
	![[Pasted image 20240511201546.png]]	


-> What if we wanted to perform artifact collection remotely and en masse? This is where EDR solutions and Velociraptor come into play.

	video-explicació setup de velociraptor

##### EXTRACTING NETWORK EVIDENCE

-> Our "Intro to traffic analysis" and "Intermediate traffic analysis" modules covered traffic capture analysis. we use tools like wireshark or tcpdump.

-> Our "Working with IDS/IPS" and "Detecting Windows Attacks with Splunk" modules covered the usage of IDS/IPS-derived data.

-> Traffic flow data, often sourced from tools like NetFlow or sFlow, provied us with a broader view of our network's behavior.

-> Lastly, our trustly firewall.

## B) EVIDENCE EXAMINATION and ANALYSIS

### B.1 Memory Forensics

-> Memory forensics, also known as volatile memory analysis is a specialized branch of digital forensics that focuses on the examination and analysis of the volatile memory (RAM) of a computer or digital device. Types of data found in RAM are:

- Network connections
- File handles and open files
- Open registry keys
- Running processes on the system
- Loaded modules
- Loaded device drivers
- Command history and console sessions
- Kernel data structures
- User and credential info
- Malware artifacts
- System configurations
- Process memory region

-> SANS's six-step memory forensics methodology:

1) Process identification and verification
	1) Enumerate all running processes
	2) Determine their origin within the OS
	3) Cross-reference with known legitimate processes
	4) Highlight any signs of DLL injection or hijacking
	5) 
2) Deep Dive into Processes Components
	1) Examine DLLs linked to the suspicious process.
	2) Check for unauthorized or malicious DLL
	3) Investigate any signs of DLL injection or hi
3) Netowrk Activity Analysis
	1) Review active and passive netowrk connections in the system's memory
	2) Identify and document external IP addressesand associated domains.
	3) Determine the nature and purpose of the communication
4) Code Injection Detection
	1) Use memory analysis tools to detect anomalies or signs of these techniques.
	2) Identify any processes that seem to occupy unusual memory spaces or exhibit unexpected behaviors.
5) Rootkit Discovery
	1) Scans for signs of rootkit activity or deep OS alterations
	2) Identify any processes or drivers operating at unusually high privileges or exhibiting stealth behaviors.
6) Extraction of Suspicious Elements
	1) Dumping the suspicious components from memory
	2) Storing them securely for subsequent examination using specialized forensics tools.


##### THE VOLATILITY FRAMEWORK
-> The prefered tool for conducting memory forensics is Volatility (open-source memory forensic framework). Està bassat en python així que ho podem executar en qualsevol plataforma que sigui compatible amb python.
Let's now see a demonstration of using Volatility v2 to analyze a memory dump saved as win7-25l5534d.vmemifying Injected Code

- Example 1 -> Identifying the Profile

	-> Profiles are essential for Volatility v2 to interpret the memory data correctly. To determine the profile that matches the OS of the memory dump we can use the "imageinfo" plugin.

- Example 2 -> Identifying Running Processes

	-> Let's see if the suggested Win7SP1x64 profile is correct by trying to list running process via the "pslist" plugin.

- Example 3 -> Identifying Netowrk Artifacts

	-> The "netscan" plugin can be used to scan for network artifacts.

- Example 4 -> Identifying Injected Code

	-> The "malfind" plugin can be used to identify and extract injected code and malicious payloads from the memory of a running process.

- Example 5 -> Identifying Handles

	-> The "handles" plugin in Volatility is used for analyzing the handles (file and object references) held by a specific process within a memory dump.

- Example 6 -> Identifying Windows Services
 
	-> The "svcscan" plugin is used for listing and analyzing Windows services running on a system within a memory dump.

- Example 7 -> Identifying Loaded DLLs

	-> The "dlllist" plugin in Volatility is used for listing the dynamic link libraries (DLLs) loaded into the address space of a specific process within a memory dump.

- Example 8 -> Identifying Hives

	-> The "hivelist" plugin is used for listing the hives (registry files) present in the memory dump of a Windows system.
	
- Example 9 -> Rootkit Analysis with Volatility v2

- Example 10 -> Memory Analysis Using Strings

### B.2 Disk Forensics

-> Having covered memory forensics, let's now shift our attention to the area of disk forensics. For incident response teams, certain functionalities stand out:

1) File Structure Insight -> Being able to navigate and see the disk's file hierarchy is crucial.
2) Hex Viewer -> For those moments when you need to get up close and personal with your data, viewing files in hexadecimal is essential.
3) web Artifacts Analysis
4) Email Crawling
5) Image Viewer
6) Metadata Analysis

-> Autopsy is a user-friendly forensics platform built atop the open-source Sleuth Kit toolset. It mirrors many features you would finde its commercial counterparts.

	(+ Setup Autopsy example)

### B.3 Rapid triage examination and Analysis Tools

##### MAC(b) Times in NTFS

-> The term MAC(b) times denotates a series of stamptimes linked to files or objects. These timestamps are pivotal as they shed light on the cronology of events or actions on a file system.

- Modified Time (M) -> Captures the last instace when the content within the file underwent modifications.
- Accessed Time (A) -> Reflects the last occasion when the file was accessed or read.
- Changed (Changege in MFT Record) (C) -> Captures the moment when the file was initially created.
- Birth Time (b) -> Represents the precise moment when the file or object was instantiated on the file system.

⚠️ All these timestamps reside in the $MFT file, located at the root of the system drive. Els atributs amb aquesta informació son: `STANDARD_INFORMATION` i `FILE_NAME`

##### General Rules for Timestamps in the Windows NTFS File System

![[Pasted image 20240513171104.png]]

##### Timestomping Investigation

-> [Timestomping](https://attack.mitre.org/techniques/T1070/006/): When adversaries **manipulate file creation times** or deploy tools for such purposes, the timestamp displayed in the file explorer undergoes modification

-> However, given our knowledge that the timestamps in the file explorer originate from the `STANDARD_INFORMATION` attribute, we can **cross-verify this data** with the timestamps from the `FILE_NAME` attribute through MFTEcmd:

````powershell-session
PS C:\~\Get-ZimmermanTools\net6>.\MFTECmd.exe -f 'C:\~\forensic_data\kape_output\D\$MFT' --de 0x16169
````

![[Pasted image 20240513173323.png]]

![[Pasted image 20240513173335.png]]

##### Filesystem-based Artifacts

1) **MFT FILE

-> El fitxer $MFT, comúnment conegut com a [Taula de Fitxers Mestra](https://learn.microsoft.com/en-us/windows/win32/fileio/master-file-table), és una part integral del [NTFS](https://learn.microsoft.com/en-us/windows-server/storage/file-server/ntfs-overview) (Sistema de Fitxers de Nova Tecnologia) utilitzat pels sistemes operatius Windows contemporanis. Aquest fitxer és fonamental per **organitzar i catalogar fitxers i directoris** en un volum NTFS. Cada fitxer i directori en aquest volum té una entrada corresponent a la Taula de Fitxers Mestra. Pensa en la MFT com una base de dades exhaustiva, **documentant meticulosament metadades i detalls estructurals** sobre cada fitxer i directori.

-> Per la informàtica forense, la MFT és un tresor d'informació. Ofereix un **registre detallat de les activitats de fitxers i directoris en el sistema**, abastant accions com la creació, modificació, eliminació i accés de fitxers. Aprofitant la MFT, els analistes forenses poden **reconstruir un cronograma detallat** d'esdeveniments del sistema i interaccions d'usuaris.

-> La MFT està estratègicament situada a la base de la unitat de sistema.

⚠️ Un tret destacat de la MFT és la seva capacitat per conservar metadades sobre fitxers i directoris, fins i tot després de la seva eliminació del sistema de fitxers. Aquesta característica eleva la importància de la MFT en l'anàlisi forense i la recuperació de dades.

	videoexemple analitzant un arxiu MFT.

**1.1 ) STRUCTURE OF MFT FILE RECORD**

-> Cada fitxer o directori en un volum NTFS està simbolitzat per un registre a la MFT. Aquests registres segueixen un format estructurat, ple d'atributs i detalls sobre el fitxer o directori associat.


![[Pasted image 20240513175056.png]]


- **File Record Header** -> Conté metadades sobre el propi registre de fitxers. Inclou camps com la signatura, el número de seqüència i altres dades administratives.
- **Standard Infromation Attribute** -> Emmagatzema metadades estàndard del fitxer com ara marques de temps, atributs del fitxer i identificadors de seguretat.
- **File Name Attribute Header** -> Conté informació sobre el nom del fitxer, incloent la seva longitud, espai de noms i caràcters Unicode.
- **Data Attribute Header** -> Descriu l'atribut de dades del fitxer, que pot ser resident (emmagatzemat dins del registre MFT) o no resident (emmagatzemat en clústers externs).
	- Dades del fitxer -> Aquesta secció conté les dades reals del fitxer, que poden ser el contingut del fitxer o referències a clústers de dades no residents. Per a fitxers petits (menys de 512 bytes), les dades poden estar emmagatzemades dins del registre MFT (resident). Per a fitxers més grans, fa referència a clústers de dades no residents al disc. Veurem un exemple d'això més endavant.
- **Additional Attributes (optional)** -> NTFS suporta diversos atributs addicionals, com ara descriptors de seguretat (SD), identificadors d'objectes (OID), nom del volum (VOLNAME), informació d'índexos i més.

-> We can see the common type of information which is stored inside these header and attributes in the image below:

![[Pasted image 20240611165010.png|600]]

a) **FILE RECORD HEADER**

*cONTINUARa...*
4) 