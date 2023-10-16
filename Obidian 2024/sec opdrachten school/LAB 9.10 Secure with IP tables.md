Doel

Het beveiligen van een host en een netwerk met behulp van IP-tables

Opdracht

Bouw het onderstaande netwerk

![[Pasted image 20231004114416.png]]

![[Pasted image 20231004114420.png]]

Gebruikte handleiding:

> [!WARNING] 
> Handleiding is bagger sommige dingen werken niet zoals beschreven

[https://linuxhint.com/configure-nat-on-ubuntu/](https://linuxhint.com/configure-nat-on-ubuntu/)

1. Wat zijn de regels in IP-tables voor de realisatie van de NAT router?  
     werk de regels hieronder uit

```
 sudo iptables -t nat -A POSTROUTING -j MASQUERADE
```
  
 

1. Forward in de NAT router de poorten voor http en https naar de www server.  
     werk de regels hieronder uit

```
sudo iptables -t nat -A PREROUTING -i enp0s8 -p tcp --dport 80 -j DNAT --to-destination 10.10.10.3:80
```

 

1. Wat is het commando (tail) om de access.log van de www server continue uit te lezen?  
     uitwerking commando

![[Pasted image 20231004114534.png]]

1. Forward in de NAT rtr één specifiek IP adres van het fysieke netwerk naar de www server met poort 22.

Uitwerking commando  
 

```
iptables -t nat -A PREROUTING -p tcp -d <extern IP> --dport 22 -j DNAT --to-destination <intern IP>:22
```

```
iptables -t nat -A POSTROUTING -p tcp -s <intern IP> --sport 22 -j SNAT --to-source <router IP>
```

1. Start een attack van het fysieke netwerk naar de www server en check dit met het tail commando (log bestand)  
     Bewijs dit met een screenshot

![[Pasted image 20231004114555.png]]
1. Zorg ervoor dat met IP tables de server wordt beveiligt tegen (D)DOS aanvallen.  
     werk de regels hieronder uit

**SYN Flood Protection:**

```
iptables -A INPUT -p tcp --syn -m limit --limit 1/s --limit-burst 3 -j ACCEPT
```

```
iptables -A INPUT -p tcp --syn -j DROP
```

Deze regels staan alleen nieuwe TCP-verbindingen toe op een snelheid van 1 per seconde met een burst-limiet van 3. Als de limieten worden overschreden, worden verdere SYN-pakketten verworpen.

**ICMP Flood Protection:**

```
iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s --limit-burst 5 -j ACCEPT
```

```
iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```

Deze regels staan slechts één ICMP echo-request-pakket per seconde toe met een burst-limiet van 5. Extra ICMP echo-request-pakketten worden verworpen.

**Limiting Connections per IP:**

```
iptables -A INPUT -p tcp --syn -m connlimit --connlimit-above 10 -j REJECT --re
```

1. Wat zijn de mogelijkheden voor het plaatsen van IP tables?  
     

Ip tabels kan geinstalleerd worden op bijna ieder linux systeem  
 

1. Wat heeft de voorkeur?

```
Ubuntu server met meerdere netwerkaarten
```

1. Zet de DDOS aanval op naar de www server en check of de firewall deze tegenhoudt.

Bewijs dit met een screenshot

![[Pasted image 20231004114713.png]]

![[image 1.png]]

**Bronnen**

[How To Build Your Own DDoS Protection With Linux & IPtables in 2021 (javapipe.com)](https://javapipe.com/blog/iptables-ddos-protection/)