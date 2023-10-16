![[acl-extended.pkt]]

Het configureren van een extended list komt overeen met de standard list. Het grote verschil zit in de uitgebreide mogelijkheden die de extended list als filtervoorwaarde kent. Zo kunnen bij de extended list de volgende filtervoorwaarden gebruikt worden:

1. Source IP addressen
2. Destination IP addressen
3. Protocol typen van laag 4: TCP, UDP, …. Deze worden in de IP header op laag 3 al aangekondigd: 6 voor TCP en 17 voor UDP
4. De applicatie / poorten: deze wordt in de header van laag 4 reeds aangekondigd: het portnummer 23 voor telnet, poort 80 voor http, poort 21 voor FTP.

Syntax Extended ACL (nrs 100 - 199)

Ip access-list 100 <<permit/deny>> <<protocol>> <<ip source>> <<wildcardmask>> <<ip destionation>><<wildcardmask>> eq <<port of services>>

Vb

Ip access-list 100 deny ip 192.168.0.2 0.0.0.0 any

Ip access-list 101 permit tcp 192.168.0.1 0.0.0.0 10.0.0.0 0.255.255.255 eq 80

De Access-list 100 - 199 staan voor extended ACL's

Configuratie nieuwe routers:

Ip access-list extended <<naam_van_acl>>

Router(config-ext-nacl)#deny ip 192.168.0.1 0.0.0.0 any

Router(config-ext-nacl)#deny ip host 192.168.0.1 any

Router(config-ext-nacl)#permit tcp 192.168.0.10 0.0.0.0 eq 80 10.0.0.0 0.255.255.255 eq 80

 ­

Opgaven

Zie voor de onderstaande opgaven bovenstaand acl-extended.pkt bestand.

- Alle verkeer van internet naar het LAN netwerk wordt geblokkeerd en de DMZ worden geblokkeerd
- Alle host mogen van buiten mogen de www1 en de ftp1 server benaderen
- Host 87.195.34.88 mag met de auth-ssh in de DMZ  communiceren op basis van poort 22
- Vanuit het LAN mag alleen host www-ftp de ssh server benaderen.
- Vanaf 188.200.240.97 mag verbinding worden gemaakt met de Windows Desktop
- Alle verkeer mag van het LAN naar het host in de DMZ communiceren
- Vanaf auth-ssh mag verbinding worden gemaakt met DC1 (Windows server) RDP
- 198.200.149.154 mag de mail server in de DMZ bereiken met de volgende protocollen: SMTP en IMAP

Werk hieronder de ACL's uit:

Benoem per router per interface steeds de bijbehorende ACL.

Router 0:

- Interface naar LAN-netwerk:

    - Toestaan van verkeer van buiten naar de www1- en ftp1-server:

        ```

        ip access-list extended LAN_IN

        permit tcp any host 10.0.10.1 eq 80

        permit tcp any host 10.0.10.2 eq 21

        ```

- Interface naar DMZ:

    - Blokkeren van verkeer van internet naar DMZ:

        ```

        ip access-list extended DMZ_IN

        deny ip any 10.0.10.0 0.0.0.255

        ```

Router 1:

- Interface naar LAN-netwerk:

    - Alleen host www-ftp mag de SSH-server benaderen:

        ```

        ip access-list extended LAN_IN

        permit tcp host 10.0.11.3 host 10.0.10.4 eq 22

        ```

- Interface naar DMZ:

    - Toestaan van verbindingen van host 87.195.34.88 naar de SSH-server in de DMZ:

        ```

        ip access-list extended DMZ_IN

        permit tcp host 87.195.34.88 host 10.0.10.4 eq 22

        ```

Router 2: Aangezien deze router niet geconfigureerd kan worden, plaatsen we hier geen ACL's. Merk op dat de exacte IP-adressen en wildcardmasks ontbreken in de bovenstaande configuraties. Zorg ervoor dat je de juiste IP-adressen en wildcardmasks invult op basis van je netwerktopologie en vereis