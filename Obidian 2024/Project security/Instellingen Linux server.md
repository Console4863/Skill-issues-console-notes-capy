tags:  [[School]]  [[IT]]
links: 

--- 
> [!INFO]
> Basis instellingen server

```
Versie:
Ubuntu-22.0.1-live-server-amd64
```

```
Yourname: natradius
Servernam: natradius
username: vogel
wachtwoord: FPitDr88
```

```
OpenSSH geinstalleerd tijdens de installatie
```

Configuratie netwerk kaart:

```
# This is the network config written by 'subiquity'
network:
  version: 2
  ethernets:
    ens18:
      dhcp4: false
      addresses:
        - 192.168.20.10/24
      nameservers:
        addresses: [10.123.3.32, 8.8.8.8]
      routes:
        - to: default
          via: 192.168.20.254
    ens19:
      dhcp4: true
#  version: 2
```

> [!INFO]
> Installatie NAT router


![[IP tables]]

> [!INFO]
> Installatie Radius server

![[Radius server linux]]

