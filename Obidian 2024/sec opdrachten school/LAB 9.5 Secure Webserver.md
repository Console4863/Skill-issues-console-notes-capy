Doel

Het doel van de opdracht is aanvallen op een server detecteren en voorkomen.

Opdracht

1. Installeer een webserver in linux

> [!INFO] 
> Voorbeeld is uit gewerkt op Lamp server

```
sudo apt install lamp-server   
```

2. Zorg ervoor dat met SSH ingelogd kan worden. Test of dit mogelijk is.  
     Log eveneens in met een fout wachtwoord.

![[Pasted image 20231004113255.png]]

```
IP server:
192.168.20.173
```

1. In welk bestand wordt de registratie van de authenticatie vastgelegd.  
     (bewijs met afbeelding)

```
/var/log/auth.log
```

![[Pasted image 20231004113341.png]]

Start vanuit Kali Linux een Brute force password attack op de server. Bewijs met een afbeelding dat er een Brute force password attack op de server heeft plaatsgevonden.

![[Pasted image 20231004113401.png]]



1. Installeer Snort en detecteer op portscan. Benader de webserver via een browser en bewijs dit met een screenshot (uitvoer van Snort).

[https://linuxopsys.com/topics/install-snort-on-ubuntu?utm_content=cmp-true](https://linuxopsys.com/topics/install-snort-on-ubuntu?utm_content=cmp-true)

![[Untitled picture.png]]

Configureer Snort zodat een aanval op port scan wordt gedetecteerd. Start vanuit Kali Linux een Christmas aanval en controleer en bewijs dit met een screenshot dat Snort deze aanval detecteert.

![[Pasted image 20231004113549.png]]

 Configureer Snort zodat een aanval op de authenticatie met ssh wordt gedetecteerd. Val de server aan met een password attack (ssh) en bewijs met een afbeelding dat Snort deze aanval detecteert.

![[image.png]]

Schrijf een beveiligings voorstel waarin zowel een portscan als een brute force password attack voorkomen kan worden. Neem in het voorstel minimaal tien items op.

```
Implementatie van een geavanceerde firewall: Een up-to-date firewall met inbraakdetectie en preventiecapaciteiten is essentieel om ongeautoriseerde toegang tot uw netwerk te voorkomen en potentiële aanvallers te detecteren.
```

```
Regelmatige patching en updates: Zorg ervoor dat alle software, besturingssystemen en applicaties op uw systemen up-to-date zijn. Dit minimaliseert de kans op kwetsbaarheden die kunnen worden misbruikt door aanvallers.
```

```
Sterke en complexe wachtwoorden afdwingen: Stel een wachtwoordbeleid in dat gebruikers dwingt om sterke en unieke wachtwoorden te gebruiken. Dit maakt het moeilijker voor aanvallers om wachtwoorden te kraken door brute force.
```

```
Twee-factor-authenticatie (2FA) implementeren: Voeg een extra beveiligingslaag toe door 2FA in te schakelen voor alle gebruikersaccounts. Dit zorgt ervoor dat zelfs als een wachtwoord wordt gekraakt, een aanvaller nog steeds een tweede authenticatiefactor nodig heeft om toegang te krijgen.
```

```
Beperk toegang tot specifieke IP-adressen: Configureer uw netwerk om alleen toegang toe te staan vanaf vertrouwde IP-adressen. Dit vermindert de blootstelling aan portscans van externe bronnen.
```

```
Gebruik van VPN (Virtual Private Network): Stel een VPN in om externe toegang tot uw netwerk mogelijk te maken. Hierdoor kunnen medewerkers veilig verbinding maken en wordt de kans op aanvallen via openbare netwerken verkleind.
```

```
Implementeer een logboeksysteem: Houd gedetailleerde logboeken bij van inkomend en uitgaand netwerkverkeer, evenals inlogpogingen. Dit stelt u in staat om verdachte activiteiten te detecteren en te onderzoeken.
```

```
Gebruik van network segmentation: Splits uw netwerk op in verschillende segmenten om de impact van een succesvolle aanval te beperken. Dit zorgt ervoor dat zelfs als een deel van uw netwerk wordt gecompromitteerd, de schade beperkt blijft.
```

**Bronnen**

[Snort for Dummies.pdf (lagout.org)](https://doc.lagout.org/Others/Snort%20for%20Dummies.pdf)

[Nmap Xmas Scan (linuxhint.com)](https://linuxhint.com/nmap_xmas_scan/)

[Cisco Switch Port Mirroring / Monitor Port Setup - YouTube](https://www.youtube.com/watch?v=d7PRD8DGoFU)

![[Pasted image 20231004114134.png]]

[2-3-3.snort.pdf (nsrc.org)](https://www.nsrc.org/workshops/2015/apricot2015/raw-attachment/wiki/Track5Agenda/2-3-3.snort.pdf)

[SNORT Demo - Network Intrusion Detection and Prevention System - Kali Linux - Cyber Security #10 - YouTube](https://www.youtube.com/watch?v=vLVdfAJ1Tr4)

![[Pasted image 20231004114121.png]]

[Blocking Brute Force Attacks Control | OWASP Foundation](https://owasp.org/www-community/controls/Blocking_Brute_Force_Attacks#)