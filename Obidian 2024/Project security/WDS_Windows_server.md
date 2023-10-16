tags: #leren #school #friesepoort  #project-security
links: https://www.yourhowto.nl/?page_id=63 , https://www.youtube.com/watch?v=0JCMzgPqtsA , <https://filestar.com/skills/iso/convert-iso-to-wim>

---

## proxmox srv 1

Proxmox IP srv 1: 192.168.20.1

## WDS server VM

Iso: en_windows_server_2019_180days.iso
Ram: 4 GB (dit is alles wat beschikbaar is)
cores: 2 (dit is genoeg)
ID: 102
Licentie: geen

hostname: WDS-server
Domain: WDS-server.tv
IP: 192.168.20.30s
Gebruiker: administartor
WW: FPitDr88

<iframe src="https://www.yourhowto.nl/?page_id"=63 width="400" height="200"></iframe>

## MDT Deployment share rules:

OSInstall=Y

SkipCapture=YES

SkipAdminPassword=YES

SkipProductKey=YES

SkipComputerBackup=YES

SkipBitLocker=YES

SkipComputerName=YES

SkipDomainMembership=YES

JoinDomain=WDS-server.tv

DomainAdmin=Administrator

DomainAdminDomain=WDS-server

DomainAdminPassword=FPitDr88

SkipUserData=YES

SkipCapture=YES

DoCapture=NO

SkipLocaleSelection=YES

SkipTaskSequence=NO

SkipTimeZone=YES

SkipApplications=YES

SkipSummary=YES

SkipBDDWelcome=YES

TimeZone=110

TimeZoneName=Europe Standard Time

## Bootstrap conf

[Settings]
Priority=Default

[Default]
DeployRoot=\\WIN-M8KPA3BP9ML\\DeploymentShare$
UserID=Gebruiker
UserDomain=WDS-Server.tv
UserPassword=FPitDr88
Keyboardlocale=en-US
SkipBDDWelcome=YES

## korte instructie install.esd naar install.wim

Hier is een korte instructie om een install.esd-bestand om te zetten naar een install.wim-bestand met behulp van een WDS-server:

1. Locatie van het install.esd-bestand:
   Zoek het install.esd-bestand op je systeem. Meestal bevindt het zich in de installatiemedia van Windows, zoals een ISO-bestand of een USB-stick met Windows-installatiebestanden. Je kunt ook de zoekfunctie van je besturingssysteem gebruiken om naar het bestand te zoeken.
2. Open een opdrachtprompt:
   Open een opdrachtpromptvenster met beheerdersrechten. Klik met de rechtermuisknop op het Startmenu en selecteer "Opdrachtprompt (Admin)" of "Windows PowerShell (Admin)".
3. Gebruik het eerste commando:
   Typ het volgende commando en druk op Enter:

   ```
   dism /Get-WimInfo /WimFile:pad_naar_install.esd
   ```

   Vervang "pad_naar_install.esd" door het daadwerkelijke pad naar het install.esd-bestand op je systeem. Dit commando toont informatie over de afbeeldingen in het install.esd-bestand, inclusief het Index-nummer dat je nodig hebt voor het volgende commando.
4. Gebruik het tweede commando:
   Typ het volgende commando en druk op Enter:

   ```
   dism /export-image /SourceImageFile:pad_naar_install.esd /SourceIndex:IndexNumber /DestinationImageFile:pad_naar_install.wim /Compress:max /CheckIntegrity
   ```
   - Vervang "pad_naar_install.esd" door het daadwerkelijke pad naar het install.esd-bestand op je systeem.
   - Vervang "IndexNumber" door het Index-nummer dat je hebt verkregen uit het vorige commando.
   - Vervang "pad_naar_install.wim" door het gewenste pad en de naam voor het nieuwe install.wim-bestand dat je wilt maken.

   Dit commando converteert het install.esd-bestand naar het install.wim-formaat met behulp van de opgegeven compressie-instelling ("max") en controleert de integriteit van het nieuwe bestand.

Na het voltooien van deze stappen heb je succesvol een install.wim-bestand gemaakt vanuit het install.esd-bestand met behulp van de opdrachten van de WDS-server. Je kunt het nieuwe install.wim-bestand nu gebruiken voor verdere implementatie of distributie via WDS.

![[Pasted image 20230705102746.png]]

![[Pasted image 20230705102832.png]]

![[Pasted image 20230705111516.png]]

![[Pasted image 20230705111538.png]]