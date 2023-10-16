# Handleiding Microsoft Deployment Toolkit 2013

_Auteur: Jurgen Kamp_

_Datum: 24-6-2016_

### Inleiding

In deze handleiding laat ik zien hoe u Microsoft Deployment Toolkit (MDT) 2013 installeert en configureert op een Windows Server 2012 R2.

In onderstaande handleiding worden de volgende onderdelen geïnstalleerd en geconfigureerd:

- Installeer en configureer Microsoft Deployment Toolkit
- Installeer Windows Deployment Services
- Installeer Windows Assessment and Deployment Kit (Windows ADK)
- Installeer Microsoft Deployment Toolkit (MDT) 2013
- Configuratie Microsoft Deployment Toolkit (MDT) 2013

## Installeer en configureer Microsoft Deployment Toolkit

Voor de voorbereiding heb ik 3 onderdelen nodig:

- Windows Deployment Services
- Microsoft Assessment And Deployment Kit (Windows ADK)
- Microsoft Deployment Toolkit (MDT) 2013

### Installeer Windows Deployment Services

**Stap 1:**

Voeg de volgende rol toe: “Windows Deployment Services” in “ServerManager”.

![[Pasted image 20231005082155.png]]
### Installeer Windows Assessment and Deployment Kit (Windows ADK)

**Stap 1:**

Download de Microsoft Assessment and Deployment Kit (ADK) die gevonden kan worden op de volgende website: https://www.microsoft.com/en-us/download/details.aspx?id=39982

Vink de volgende onderdelen aan: **Deployment Tools, Windows Preinstallation Environment (Windows PE), Imaging and Configuration Designer (ICD) en User State Migration Tools (USMT)** en klik op **Install:**

> [!WARNING] >
> PE heeft een los installatie programma nodig
>

![[Pasted image 20231005083126.png]]

### Installeer Microsoft Deployment Toolkit (MDT) 2013

**Stap 1:**

Download de Microsoft Deployment Toolkit (MDT) 2013 die gevonden kan worden op de volgende website: https://www.microsoft.com/en-us/download/details.aspx?id=54259

Klik op **MicrosoftDeploymentToolkit2013_x64.msi:**

![[Pasted image 20231005084141.png]]

### Configuratie Microsoft Deployment Toolkit (MDT) 2013



Een nieuwe **Deployment Workbench** is gecreëerd. Start de **Deployment Workbench (NEW):**

![[Pasted image 20231005084327.png]]

Als u het programma voor het eerst start, ziet u het overzicht van MDT 2013**:**

**Stap 5:**

![[Pasted image 20231005084445.png]]

Klik met uw rechtermuisknop op **Deployment Shares** in het linker navigatievenster op **New Deployment Share:**

**Stap 6:**

![[Pasted image 20231005084539.png]]

Klik op **next:**

**Stap 7:**

![[Pasted image 20231005084623.png]]

Verander de **Share name** naar **DeploymentShare$**, klik daarna op **next:** 

**Stap 8:**

![[Pasted image 20231005084645.png]]

Klik **next:**

**Stap 9:**

![[Pasted image 20231005084708.png]]

Zet alle vinkjes uit en klik **next:**

**Stap 10:**

![[Pasted image 20231005084728.png]]

Check of de details kloppen en klik **next:**

**Stap 11:**

![[Pasted image 20231005084754.png]]

Klik **Finish:**

Open **File Explorer:**

![[Pasted image 20231005084835.png]]

Open **Local Disk (C:):**

**Stap 15:**

![[Pasted image 20231005084903.png]]

Klik met uw rechtermuisknop op **DeploymentShare:**

Klik op **Properties:**

**Stap 17:**

![[Pasted image 20231005085125.png]]

Ga naar het tablad sharing en Klik op **Advanced Sharing…:**

**Stap 18:**

![[Pasted image 20231005085150.png]]

Klik op **Permissions:**

**Stap 19:**

![[Pasted image 20231005085258.png]]

Kijk of **Everyone** is toegevoegd en **Full Control** heeft (zo niet: klik op **Add…):**

**Stap 20:**

![[Pasted image 20231005085416.png]]

In de **Security** tab van de share, voegt u **Users** en **Domain Users** toe. U geeft ze de volgende rechten: **Read & Execute, List folder contents en Read:**

**Stap 21:**

![[Pasted image 20231005085503.png]]

Terug in “the Deployment Workbench”, klik u met de rechtermuisknop op **MDT Deployment Share** en daarna op **Properties:**

**Stap 22:**

![[Pasted image 20231005085535.png]]

Onder de **Rules** tab, voegt u de volgende rij met opties toe onder het kopje [Default] :

OSInstall=Y

SkipCapture=YES

SkipAdminPassword=YES

SkipProductKey=YES

SkipComputerBackup=YES

SkipBitLocker=YES

SkipComputerName=YES

SkipDomainMembership=YES

JoinDomain=testwds.local

DomainAdmin=Administrator

DomainAdminDomain=testwds

DomainAdminPassword=Welkom01

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

![[Pasted image 20231005103317.png]]

De opties zijn toegevoegd, klik nu op **Edit Bootstrap.ini:**

**Stap 23:**

[![048](https://web.archive.org/web/20200807095257im_/http://www.yourhowto.nl/wp-content/uploads/2016/04/048.png)](https://web.archive.org/web/20200807095257/http://www.yourhowto.nl/wp-content/uploads/2016/04/048.png)

Onder het kopje [Default] voegt u de volgende opties toe:

DeployRoot=\\WIN-M8KPA3BP9ML\\DeploymentShare$
UserID=Gebruiker
UserDomain=WDS-Server.tv
UserPassword=FPitDr88
Keyboardlocale=en-US
SkipBDDWelcome=YES


> [!INFO] >
> Sla vervolgens het documentje op
>

Volgende, we importeren het Besturingssysteem voor **Windows 10. om dit te doen, klikt u met de rechtermuisknop operating system en vervolgens op import operating system.

**Stap 29:**

![[Pasted image 20231005111013.png]]
In de Deployment Workbench, klikt u met uw rechtermuisknop op **Operating System** en klikt u op **Import Operating System:**

**Stap 30:**

![[Pasted image 20231005111202.png]]

Selecteer WIM File en selecteer de locatie:**

**Stap 31:**

[![056](https://web.archive.org/web/20200807095257im_/http://www.yourhowto.nl/wp-content/uploads/2016/04/056.png)](https://web.archive.org/web/20200807095257/http://www.yourhowto.nl/wp-content/uploads/2016/04/056.png)

Typ **E:\** om de Installatie media (ISO) te selecteren. Klik daarna **next:**

**Stap 32:**

![[Pasted image 20231005111249.png]]

Klik daarna op **next:**

**Stap 33:**

![[Pasted image 20231005111336.png]]

Maak de naam aan van de share

**Stap 34:**

![[Pasted image 20231005111412.png]]

Klik daarna op next:

**Stap 35:**


zodra de installatie is voltooid druk op finish 

Klik met uw rechtermuisknop op **Task Sequence** en klik daarna op **New Task Sequence:**

**Stap 37:**

![[Pasted image 20231005111636.png]]

Typ: **Deploy8.1** bij Task sequence ID: en **Deploy Windows 8. 1 x64** bij Task sequence name**:**

**Stap 38:**

![[Pasted image 20231005111656.png]]

Selecteer **Standard Client Task Sequence** en klik **next:**

**Stap 39:**

![[Pasted image 20231005111720.png]]

Selecteer de ISO naar keuze 

**Stap 40:**

![[Pasted image 20231005111757.png]]

Selecteer **Do not specify a product key at this time.** Klik daarna op **next:**

**Stap 41:**

![[Pasted image 20231005111848.png]]

Voer een **Naam**, **organisatie** en **startpagina** in. Klik **next:**

**Stap 42:**

![[Pasted image 20231005111914.png]]

Voer een administratorswachtwoord in. Klik daarna op **next:**

**Stap 43:**

![[Pasted image 20231005111933.png]]

Klik **Next:**

**Stap 44:**

![[Pasted image 20231005111954.png]]

Klik **Finish:**

**Stap 45:**
![[Pasted image 20231005112104.png]]


Nu gaan we de “task sequence” wijzigen, hierdoor kunnen windows updates worden geïnstalleerd.

Klik met uw rechtermuisknop op **Deploy Windows 8.1 x64** klik daarna op **properties:**

**Stap 46:**

![[Pasted image 20231005112138.png]]

Ga naar het tabje **Task Sequence** bovenin**:**

**Stap 47:**



Onder **State Restore** staan 2 onderdelen voor Windows Update die allebei uitgeschakeld zijn (vinkje is te vinden onder het tabje “**options**“). Verwijder het vinkje bij **Disable this step.** Klik **OK** om de wijzigingen op te slaan**:**

**Stap 48:**

![[Pasted image 20231005112225.png]]

Klik met uw rechtermuisknop op **MDT Deployment Share (C: Deploymentshare)** klik daarna op **Update Deployment Share:**

**Stap 49:**

![[Pasted image 20231005112315.png]]

Klik **Next:**

**Stap 50:**

![[Pasted image 20231005112336.png]]

Klik **Next**:

**Stap 51:**

![[Pasted image 20231005112612.png]]

Als het proces succesvol is afgerond klikt u op **Finish:**

**Stap 52:**

![[Pasted image 20231005113015.png]]

In Windows Server 2012 R2, klik op het **Startsymbool** (Links onderin het scherm)**:**

**Stap 53:**


![[Pasted image 20231005113209.png]]

Open **Windows Deployment Services:**

**Stap 55:**


![[Pasted image 20231005113314.png]]
Klik met de rechtermuisknop op de servernaam en klik daarna op **Configure Server:**

**Stap 56:**

![[Pasted image 20231005113240.png]]

Klik **Next:**

**Stap 57:**

![[Pasted image 20231005113334.png]]

Selecteer **Integrated with Active Directory** en klik op **Next:**

**Stap 58:**

![[Pasted image 20231005113407.png]]

Selecteer de locatie waar u de **RemoteInstall** folder wilt plaatsen en klik op **next:**

**Stap 59:**

![[Pasted image 20231005113442.png]]

Selecteer “**Do not listen on DHCP and DHCPv6 ports**” **en** “**Configure DHCP options for Proxy DHCP**“. Klik hierna op **next:**

**Stap 60:**

![[Pasted image 20231005113504.png]]

Selecteer **Respond to all client computer (known and unknown)**. Klik hierna op **next:**

**Stap 61:**

![[Pasted image 20231005113533.png]]

Klik **Finish:**

**Stap 62:**

![[Pasted image 20231005113603.png]]

Klik met uw rechtermuisknop op **Boot Images** en kies voor **Add Boot Image…:**

**Stap 63:**

![[Pasted image 20231005113655.png]]

Ga naar de gedeelde locatie van de deploymentshare (**\\servernaam\deploymentshare$\Boot).**

Kies nu het x64 besturingssysteem: **LiteTouchPE_x64.wim** en klik op **open:**

**Stap 64:**

![[Pasted image 20231005113713.png]]

Klik **Next:**

**Stap 65:**

![[Pasted image 20231005113730.png]]

Klik **next:**

**Stap 67:**

![[Pasted image 20231005113807.png]]

De boot image is aangemaakt! Klik op **Finish:**

**Stap 68:**

![[Pasted image 20231005115023.png]]



