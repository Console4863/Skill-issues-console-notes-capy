
1. `show version`: Toon informatie over de router/switch, waaronder het model, besturingssysteemversie en configuratie.
2. `show running-config`: Toon de huidige actieve configuratie.
3. `show startup-config`: Toon de opgeslagen opstartconfiguratie.
4. `show interfaces`: Toon informatie over netwerkinterfaces.
5. `show ip route`: Toon de routingtabel.

**Interface-configuratie:** 6. `interface [interface-type] [interface-nummer]`: Ga naar de configuratiemodus van een specifieke interface.

7. `ip address [IP-adres] [subnetmasker]`: Wijs een IP-adres toe aan een interface.
8. `description [beschrijving]`: Voeg een beschrijving toe aan een interface.

**VLAN-configuratie:** 9. `show vlan brief`: Toon een overzicht van VLAN's op een switch.

10. `vlan [VLAN-nummer]`: Ga naar de configuratiemodus van een VLAN.
11. `name [VLAN-naam]`: Geef een naam aan een VLAN.
12. `switchport mode [access/trunk]`: Stel de modus van een switchpoort in (toegang of trunk).
13. `switchport access vlan [VLAN-nummer]`: Koppel een switchpoort aan een VLAN (toegangspoort).

**Beveiliging en Access Control:** 14. `enable secret [wachtwoord]`: Stel het enable-wachtwoord in.

15. `line vty 0 15`: Ga naar de VTY-lijnconfiguratiemodus.
16. `password [wachtwoord]`: Stel een wachtwoord in voor console- of VTY-toegang.
17. `access-list [nummer] permit/deny [bron] [bestemming]`: Maak een toegangslijstregel om verkeer te filteren.
18. `crypto key generate rsa`: Genereer RSA-sleutels voor SSH-toegang.

**Diagnostiek en Troubleshooting:** 19. `ping [IP-adres]`: Voer een ping-test uit naar een IP-adres.

20. `traceroute [IP-adres]`: Voer een traceroute-test uit naar een IP-adres.
21. `show interfaces [interface]`: Toon gedetailleerde informatie over een specifieke interface.
22. `debug [protocol] [gebeurtenis]`: Schakel debugging in voor specifieke netwerkprotocollen of gebeurtenissen.

**Opslag en Bestandsbeheer:** 23. `show flash`: Toon informatie over de flash-opslag.

24. `dir`: Toon bestanden in de huidige directory.
25. `copy [bron] [bestemming]`: Kopieer bestanden van en naar de router/switch.

**Opslaan en Herstellen van Configuratie:** 26. `write memory`: Sla de actieve configuratie op naar NVRAM.

27. `copy running-config startup-config`: Kopieer de actieve configuratie naar de opstartconfiguratie.
28. `reload`: Herstart de router/switch.

**Systeembeheer:** 29. `clock set [uur:minuut:seconde] [maand dag jaar]`: Stel de systeemklok in.

30. `banner motd [tekst]`: Voeg een bannerbericht voor aanmelding toe.