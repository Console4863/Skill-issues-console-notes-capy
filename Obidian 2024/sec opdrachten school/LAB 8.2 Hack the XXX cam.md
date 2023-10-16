![[Pasted image 20231004115845.png]]


Doel

Doel van de opdracht is het achterhalen van het wachtwoord van een IP camera, met een wachtwoordlijst.

Opdracht

Om een systeem te hacken is het belangrijk eerst een methode te bedenken om te hacken! Dit is een stappenplan. Het stappenplan van deze opdracht is als volgt:

Stappenplan (globaal)

1. Vind het IP adres van de webcam
2. Vind open poorten van de webcam
3. Richt een bruteforce attack op de webcam
4. Login met gebruikersnaam en wachtwoord op de webcamera  
     

Stappenplan(detail)

1. Verbind de camera in het netwerk
2. Start Kali linux op en verbind deze met hetzelfde netwerk als de camera
3. Ga na wat het IP adres is van het netwerk
4. Onderzoek met nmap welke ip addressen in het netwerk zitten  

   Gebruik hiervoor de link hieronder of de ip scanner uit [[EXE's]]

    [https://www.cyberciti.biz/networking/nmap-command-examples-tutorials/](https://www.cyberciti.biz/networking/nmap-command-examples-tutorials/) 
5. Scan met het commando nmap het device af op openstaande poorten  
    [https://www.cyberciti.biz/networking/nmap-command-examples-tutorials/](https://www.cyberciti.biz/networking/nmap-command-examples-tutorials/) #15
6. (indien nodig? Zoek op internet default gebruikersnaam van xxx.CAM)
7. Achterhaal met hydra het wachtwoord a.d.v. een password list.  
    Hydra -l username -P password wachtwoordlijst -V ip-address http-get /

tip: maak gebruik van de wachtwoordlijst rockyou.txt (Kali Linux → /usr/share ).

1. Ga naar de website van de xxx.CAM en login met gevonden username en password.
2. Verander het password door een gekozen password uit rockyou.txt.
3. Achterhaal opnieuw het wachtwoord met behulp van het rockyou.txt bestand.

![[Pasted image 20231004115917.png]]

![[Pasted image 20231004115921.png]]