Beveilig het systeem tegen een x-mas attack

Als de TCP flaggen (URG,FIN,PSH) staan op een TCP frame het is een xmas attack

Icmp (ping) uitschakelen op de host kan met het volgende commando:

iptables -A INPUT -p icmp --icmp-type echo-request -j DROP

Dit commando zorgt er voor dat er niet meer gepingt kan worden naar de desbetrevende host. Het is nog wel mogelijk om te pingen vanuit de host naar een andere host

```
ping vanaf kali naar debian
```

![[Pasted image 20231004113929.png]]

```
Ping vanuit debian naar kali
```

![[Pasted image 20231004113943.png]]

```
Commando om te voorkomen dat je host kan worden gevonden door een nmap scan:

iptables -A OUTPUT -p tcp --tcp-flag ALL FIN,PSH,URG -j DROP
```

```
Goed om te weeten dat port 80 openstaat op de host waar we xmas willen voorkomen.
```

![[Pasted image 20231004114024.png]]

**Bronnen**

[use iptables to prevent xmas null and fin scan with nmap](https://www.youtube.com/watch?v=deCNcorwDcQ)

![[Pasted image 20231004114048.png]]

![[Pasted image 20231004114052.png]]