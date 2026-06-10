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

