Doel 

Het doel van de opdracht is het achterhalen van een WiFi WEP wachtwoord met een eigen wordlist 

Theorie 

Vijf fasen volgens CeH  

1. Reconnaissance (verkenning) voorbeelden - social enginering - dumpster diving - sniffing 
2. Scanning (meer informatie verkrijgen door scans) beeld krijgen van het netwerk en de zwakheden ervan 
3. Gainning access (toegang krijgen) Toegang krijgen tot het netwerk (bedraad / onbedraad) dmv een exploit, DOS (Denial of Services), session Hjacking 
4. Maintainning Access (zorgen voor permanente toegang) inzetten van: rootkits, backdoors en trojans, beveiligen van het systeem zodat andere crackers het systeem niet over kunnen nemen -> zombie systeem 
5. Covering tracks (voetsporen ofwel bewijsmateriaal verwijderen op het gekraakte systeem maar ook op de eigen systemen 

WIFI netwerk theorie 

Authenticatie / authorisatie 

versleuteling 

WiFi netwerken 

|   |   |   |
|---|---|---|
|Type netwerk|aanvalsplan|Praktisch|
|Open netwerk|Geen, het netwerk is open en toegankelijk|-|
|verborgen|Eerst hidden BSSID achterhalen daarna||
|WPS|Zoveel mogelijk packets afvangen en systeem||
|WEP|In de handshake zit de PSK <br><br>Zoveel mogelijk packets afvangen en system laten analyseren. <br><br>Optioneel: De verbinding tussen het AP en de client geforceerd verbreken zodat de client zich opnieuw moet aanmelden op het AP.||
|WPA/WPA2|Handshake afvangen (eventueel door geforceerd de verbinding tussen client en AP te verbreken). Daarna aan de hand van de wachtwoordlijst het wachtwoord achterhalen.||
|Radius|Niet mogelijk om de wachtwoorden te achterhalen. Elke gebruiker wordt geautoriseerd op de radius server.||

Praktisch  

Installatie en configuratie van het WiFi AP: 

- Encryptie => WEP 
- PSK => een eigen te kiezen wachtwoord 
- WAN verbinding (via NAT router – IP 192.168.0.248/255.255.255.0, IP DNS 10.110.2.2, 10.110.2.3) 

Fase 1 -> Reconnaissance  

 kal

Fase 2 -> Scanning 

In deze fase wordt het netwerk gescand. Hiervoor is een aparte adapter nodig die in monitor mode gezet kan worden. 

1. Koppel de adapter aan het systeem 
2. Koppel de adapter via de settings (USB) van virtualbox aan je VM (kali) 
3. Controleer wat de naam van de adapter is iwconfig

![[Pasted image 20231004120336.png]]

1. Zet de adapter in monitor mode airmon-ng start naam_adapter 
2. Controleer wat de naam van de adapter is geworden iwconfig

![[Pasted image 20231004120346.png]]

1. Scan het netwerk en noteer de bevindingen airodump-ng naam_adapter_mon0  

1. Noteer welke netwerk zijn gevonden

![[Pasted image 20231004120400.png]]

Fase 3 -> Gainning Access 

Aan de hand van flowchart (komt nog) bepalen van aanvalsplan 

WEP kraken 

Dump maken van het netwerkverkeer (liefst client en AP) naar een bestand 

airodump-ng naam-adapter_mon0 –bssid mac-address –c channel –w output-file 

Gelijktijdig verbinding tussen client en AP verbreken (zodat de client zich opnieuw aanmeld – authentication) 

aireplay-ng naam-adapter_mon0 –0 3 –a mac-address-AP –c mac-client 

Dump van het netwerkverkeer stoppen 

Analyse van het bestand waar de authenticatie inzit. 

Aircrack-ng capturefile.cap

![[Pasted image 20231004120415.png]]

Fase 4 -> Maintaining Access  

Maak (indien mogelijk) een nieuw gebruikers account met wachtwoord 

Verander het oude wachtwoord 

Wat zijn de mogelijkheden op het device? 

Is het mogelijk om een sombie systeem te maken? 

Fase 5 -> Covering tracks 

Zorg ervoor dat de sporen worden uitgewist, denk hierbij aan: 

- Sporen op het eigen systeem 
- Sporen op het remote systeem 

Welke sporen zijn gewist op het local systeem? 

Welke sporen zijn gewist op het remote systeem?

![[Pasted image 20231004120426.png]]