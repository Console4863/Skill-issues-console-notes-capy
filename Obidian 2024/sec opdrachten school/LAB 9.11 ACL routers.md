
Acces Control List (ACL)

Inleiding:

Bij het opzetten van een netwerk moet ook aan de beveiliging van het netwerk worden gedacht. Alle verkeer wat niet wenselijk is moet op een of andere manier buiten het netwerk worden gehouden. Dit betekent dat je restricties moet opleggen. Hierbij kun je denken aan een firewall. In een router zit ook een soort van firewall. Je kunt op een router verkeer afkomstig van of gaande naar een netwerk blokkeren. Dit doe je doormiddel van een Acces Control List. Een standaard ACL kan alleen maar IP adressen blokkeren. Extended ACLs kunnen zelfs op poort niveau blokkeren. Dit betekent dat wanneer op een computer een webserver en een ftp server draait, dat bijvoorbeeld de webserver wel bereikbaar is terwijl de FTP server niet bereikbaar is. In deze opdracht gaan we bezig met zowel de standaard als naar de extended ACLs.

Opdracht 1: Access list Algemeen

Een router kan geconfigureerd worden met Acces lists, ACL's. Hierdoor kunnen sommige pakketten tegengehouden worden (gefilterd). Het criterium voor filtering kan zijn:

1. het IP addres
2. het poort nummer (bijvoorbeeld 80 voor HTTP)
3. het protocol op laag 4 (TCP of UDP)

Ook kunnen frames gefilterd worden die

1. updates van het routing protocol bevatten.

De eenvoudigste manier is 1: op basis van het IP addres. Dit wordt standaard ACL genoemd. Als de uitbreiding met 2,3 of 4 gebruikt wordt, is er sprake van Extended ACL

Onderstaande tekening illustreert een voorbeeld van een standaard ACL

![[Pasted image 20231004114913.png]]
Stel dat een packet van net 193.20.21.0 binnenkomend bij S0 niet doorgegeven mag worden naar S1 dan zijn er 2 mogelijkheden:

Geval 1: inbound

```
Router (config)#access-list 2 deny 193.20.21.0 0.0.0.255

Router (config)#access-list 2 permit any

Router (config)#int S0

Router (config_if)#IP access-group 2 in
```

Geval 2: outbound

```
Router (config)#access-list 3 deny 193.20.21.0 0.0.0.255

Router (config)#access-list 3 permit any

Router (config)#int S1

Router (config_if)#IP access-group 3 out
```

Als we geval 1 nader bekijken zijn de volgende elementen herkenbaar:

Eerst wordt de ACL gedefinieerd (list 2) en vastgelegd wat er geweigerd (deny) moet worden. Regel 1. In dit geval alles wat het IP adres 192.21.21.x heeft. De laatste 8 bits (x) doen er niet toe.

Vervolgens moet meegedeeld worden wat er met de rest gebeurt: regel 2 permit any

Tenslotte worde in regel 3 en 4 de interface en de richting vastgelegd: S0 in en inkomend verkeer.

Bij geval 2 wordt nauwkeuriger gewerkt: pakketten van 193.20.21.0 kunnen wel doorgegeven worden naar EO. Een nadeel is dat pakketten die door de outbound ACL worden geworpen, toch de processor tijd van de router gebruiken.

Bij de voorbeelden staat telkens een wildcard: 0.0.0.255 genoemd. Dit wordt in paragraaf 2 besproken.

De voorbeelden tonen een ACL die het source adres als criterium heeft: Dit zijn de standaard ACL's die in paragraaf 3 worden besproken. De uitgebreidere ACL's Extended ACL's komen bij paragraaf 4 aan de orde. De afsluitende paragraaf bevat enkele opgaven.

Opdracht 2: Wildcard

Geval 1: inbound

```
Router (config)#access-list 2 deny 193.20.21.0 0.0.0.255

Router (config)#access-list 2 permit any

Router (config)#int S0

Router (config)#IP access-group 2 in

De waarde 0.0.0.255 komt overeen met 00000000.00000000.00000000.11111111
```

De plek waar een "0" staat moet het betreffende bitje overeenkomen met de voorwaarde in 192.20.21.0. Bij de plek waar een "1" staat hoeft geen "match" te bestaan: voor deze plekken is een "wildcard" verstrekt. Komt er een pakket binnen met source adres 193.20.21.234, dan voldoet dit aan de deny voorwaarden en zal weggegooid worden. Het source adress 193.20.20.12 voldoet niet aan de voorwaarden voor "denial" en wordt doorgelaten.

Het wildcard masker dekt nu precies de bits van de net-id; dit is echter niet noodzakelijk! Een bit combinatie waarbij ook host-id bits zijn betrokken kan door de wildcard omschreven worden. Een wildcard 0.0.0.127 controleert de eerst 25 bits, terwijl de laatste 7 bits er niet toe doen.

Probeer onderstaande tabel compleet te maken: het IP adres in de access-list commando is x.x.x.x, de acces list wildcard is y.y.y.y

Van uit gaant dat het de Denail regels is zo niet ins het anders om.

|   |   |   |   |
|---|---|---|---|
|Binnen komt|x.x.x.x|y.y.y.y|Denial of niet|
|1.55.88.111|1.55.88.4|0.0.0.0|Denail|
|1.55.88.111|1.55.88.0|0.0.0.255|Denail|
|1.55.56.7|1.55.0.0|0.0.255.255|Denail|
|5.88.22.5|0.0.0.0|255.255.255.255|Niet|
|33.1.1.1|1.1.1.0|32.48.0.255||

Opdracht 3: Standard Acces List

De ACL kan vaak op verschillende manier geconfigureerd worden: op verschillende interfaces, op verschillende routers, inboud of outband, ….. Als algemene regel geld: De standaard ACL zo dicht mogelijk bij de bestemming plaatsen.

Onderstaande voorbeeld moet dit illustreren:

Voorbeeld 1:

Veronderstel dat de Ne-host niet met de Be-computers mogen praten. Dit zou als volgt geconfigureerd kunnen worden:

```
Router-Ne(config)#access-list 1 deny 10.1.2.0 0.0.0.255

Router-Ne(config)# access-list 1 permit any

Router Ne(config)#int S1

Router-Ne(config)#ip access-group 1 out
```

Als de verbinding Be-Ne niet meer werkt en het verkeer van Ne naar Be via Router Lux gaat, zal de restrictie niet meer werken omdat S1 niet meer meedoet

Beter is om de Standaard ACL zo dicht mogelijk bij de bestemming te plaatsen, in dit geval bij E0 van Router-Be

```
Router-Ne(config)#access-list 1 deny 10.1.2.0 0.0.0.255

Router-Ne(config)# access-list 1 permit any

Router Ne(config)#int E0

Router-Ne(config)#ip access-group 1 out
```

Voorbeeld 2:

Veronderstel dat host Be1 niet met Lux-hosts mag praten:

```
Router-Be(config)#access-list 2 deny host 10.1.2.1

Router-Be(config)#access-list 2 permit any

Router Be(config)#int S0

Router-Be(config)#ip access-group 2 out
```

Wat is het nadeel van deze oplossing?

Conclusie:

1. Standaard ACL's hebben alleen betrekking op het source IP adres

2. De standaard ACL moet zo dicht mogelijk bij de bestemming worden geplaatst

Praktische opdracht Standaard ACL:

Voorbeeld tekening:

Van het bovenstaande netwerk zijn een aantal restricties in het netwerk verkeer. Geef van elke restrictie waar je de ACL plaatst en waarom. Werk als tweede de ACL uit in het verslag:

Restrictie 1:

Verkeer van het LAN netwerk van Berlijn mag niet naar het LAN netwerk van Amsterdam

Mogelijke plaatsen ACL: Tussen het publieke en Lan netwerk van amsterdam

Keuze volgens plaats ACL: Tussen het publieke en Lan netwerk van amsterdam

Ip adress Amsterdam: 17.27.25.0 /24

Ip adress Berlijn: 13.1.2.0 /24

Uitwerking ACL:

Router(config)#access-list 1 deny 13.1.2.0 0.0.0.255

Restrictie 2:

Vanaf het LAN network in Amsterdam mogen:

- de oneven computers niet met de host van Lux communiceren

Ip Lan netwerk Amsterdam: 17.27.25.0

Ip PC van Lux 17.27.25.100

Mogelijke plaatsen ACL: Tussen het lan netwerk van amsterdam en de pc van Lux

Keuze volgens plaats ACL: Tussen het lan netwerk van amsterdam en de pc van Lux

Uitwerking ACL:

Router(config)#access-list 2 deny host 17.27.25.100

Restrictie 3:

Ip parijs: 20.32.25.0 /24

Ip Amsterdam 17.27.25.0 /24

IP host lux 17.27.25.100 /24

Vanaf het LAN network in Parijs mogen:

- de computers onder de 128 niet communiceren met host van Amsterdam
- de computers boven 128 niet communiceren met host van Lux

Mogelijke plaatsen ACL: Tussen het publieke en Lan netwerk van amsterdam

En tussen het Lan netwerk en de host van Lux

Uitwerking ACL:

```
tussen het publieke en Lan netwerk van amsterdam

Router(config)#access-list 1 permit 20.32.25.0 0.0.0.127

tussen het Lan netwerk en de host van Lux

Router(config)#access-list 1 deny 20.32.25.0 0.0.0.127
```

Restrictie 4:

Van vanaf LAN network in Parijs mogen:

- de computers met oneven nummers niet communiceren met de FTP server
- en even computers niet communiceren met de www server

Mogelijke plaatsen ACL:

Keuze volgens plaats ACL:

Uitwerking ACL:

Opdracht 4: Extended Acces List

Bij het configureren komt een extended list aardig overeen met de standard list. Het grote verschil zit in de uitgebreide criteria die de extended list als filtervoorwaarde kent. Zo kunnen bij de extended list de volgende filtervoorwaarden gebruikt worden:

1. Source IP addressen
2. Destination IP addressen
3. Protocol typen van laag 4: TCP, UDP, …. Deze worden in de IP header op laag 3 al aangekondigd: 6 voor TCP en 17 voor UDP
4. De applicatie: deze wordt in de header van laag 4 reeds aangekondigd: het portnummer 23 voor telnet, poort 80 voor http, poort 21 voor FTP.

Voorbeeld 1:

```
Veronderstel dat Ne-hosts niet met de Be-hosts via telnet mogen praten:

Router-Ne(config)#access-list 101 deny ip 10.1.3.0 0.0.0.255 10.1.2.0 0.0.0.255 eq 23

Router-Ne(config)# access-list 101 permit ip any any

Router-Ne(config)#int S1

Router-Ne(config)#ip access-group 101 out
```

Je herkent hierbij de syntax:

```
Access-list {100-199}{permit/deny} protocol source address[source mask][operator operand] destination address [destination mask] [operator operand] [established]
```

Ga na op welke nummering de verschillende lists lopen:

```
Standaard

Extended list ­

IPX
```

Voorbeeld 2:

Veronderstel dat in bovenstaande figuur aan de volgende voorwaarden moet worden voldaan:

- 10.1.1.2 is de webserver en moet voor iedereen bereikbaar zijn;
- UDP clients en servers mogen niet met 10.1.1.1 werken als ze bij de bovenste helft van de toegestane IP-adressen van een subnet horen
- Be en Lux mogen alleen packets uitwisselen via de seriële link
- Lux 128 en Lux 130 mogen met alle hosts verbinding maken, behalve met host Ne2

Dit moet op verschillende routers geconfigureerd worden. Hier volgt een uitwerking voor router-Be

```
Access-list 110 permit tcp any host 10.1.1.2 eq www

Access-list 110 deny udp 0.0.0.128 255.255.255.127 host 10.1.1.1

Access-list 110 deny ip 10.1.2.0 0.0.0.255 10.1.3.0 0.0.0.255

Access-list 110 permit ip any any

Access-list 111 permit tcp any host 10.1.1.2 eq www

Access-list 111 deny udp 0.0.0.128 255.255.255.127 host 10.1.1.1

Access-list 111 permit ip any any

Int S0

Ip access-group 110

Int S1

Ip access-group 111
```
Ga nu zelf de access-list configureren voor router-lux