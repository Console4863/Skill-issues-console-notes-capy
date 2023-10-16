tags: #leren #school #netwerken 
links: 

---

## GPT antwoord

Om de ACL's voor de gegeven opgaven uit te werken, moeten we per router en interface de bijbehorende ACL configureren. Hieronder geef ik de uitwerking voor elke opgave:

Router 0:
- Interface naar LAN-netwerk:
  - Toestaan van verkeer van buiten naar de www1- en ftp1-server:
    ```
    ip access-list extended LAN_IN
    permit tcp any host <IP-www1-server> eq 80
    permit tcp any host <IP-ftp1-server> eq 21
    ```

- Interface naar DMZ:
  - Blokkeren van verkeer van internet naar DMZ:
    ```
    ip access-list extended DMZ_IN
    deny ip any <IP-DMZ-netwerk> <wildcardmask-DMZ-netwerk>
    ```

Router 1:
- Interface naar LAN-netwerk:
  - Alleen host www-ftp mag de SSH-server benaderen:
    ```
    ip access-list extended LAN_IN
    permit tcp host <IP-www-ftp> host <IP-SSH-server> eq 22
    ```

- Interface naar DMZ:
  - Toestaan van verbindingen van host 87.195.34.88 naar de SSH-server in de DMZ:
    ```
    ip access-list extended DMZ_IN
    permit tcp host 87.195.34.88 host <IP-SSH-server> eq 22
    ```

Router 2:
Aangezien deze router niet geconfigureerd kan worden, plaatsen we hier geen ACL's.

Merk op dat de exacte IP-adressen en wildcardmasks ontbreken in de bovenstaande configuraties. Zorg ervoor dat je de juiste IP-adressen en wildcardmasks invult op basis van je netwerktopologie en vereisten.

## bewerkt 
Om de ACL's voor de gegeven opgaven uit te werken, moeten we per router en interface de bijbehorende ACL configureren. Hieronder geef ik de uitwerking voor elke opgave:

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

Router 2:
Aangezien deze router niet geconfigureerd kan worden, plaatsen we hier geen ACL's.

Merk op dat de exacte IP-adressen en wildcardmasks ontbreken in de bovenstaande configuraties. Zorg ervoor dat je de juiste IP-adressen en wildcardmasks invult op basis van je netwerktopologie en vereisten.