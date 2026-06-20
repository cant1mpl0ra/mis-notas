
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

Hi han comandes que helo no funcione i aleshores has d'utilitzar /?

[ss64](https://ss64.com/nt/) Is a handy quick reference for anything command-line related, including cmd, PowerShell, Bash, and more.

Comandes explicades: cls, doskey

`doskey history` --> Mostra l'historial de comandes

### System Investigation

Absoulte vs Relative PATH

Comandes explicades: tree

We can utilize the `/F` parameter with the tree command to see a listing of each file and the directories along with the directory tree of the path.
#### Interesting Directories






























