---
title: Secure the switch
tags: [Import-6cdc]
created: '2023-02-20T10:38:40.000Z'
modified: '2023-03-21T10:48:47.968Z'
---

> [!INFO] >
> Fa 0/1 - 0/23 - access ports
> Fa 0/24 - DHCP server
> gi 0/1 - go 0/2 - trunk ports

```
Configuratie Acces ports

Switch(config)#interface range fastEthernet 0/1 - 23
Switch(config-if-range)#switchport mode access
Switch(config-if-range)#no shutdown
Switch(config-if-range)#exit
```

```
Configuratie trunk ports

Switch(config)#interface range gigabitEthernet 0/1 - 2
Switch(config-if-range)#switchport mode trunk
Switch(config-if-range)#no shutdown
Switch(config-if-range)#exit
```

> [!warning] >
> Secure toegang
> 

> [!info] >
>ip domain-name skill.local
> aanmaken van een rsa key 2048
> username Admin password Str0ng3rP@55w0rd
> ssh version toekennen aan max 3 vty sessies
> 

```
Configuratie IP domein naam

skill(config)#ip domain-name skill.local
```

> [!warning] >
> Hostename moet veranderd worden voor RSA geconfigureerd kan worden

```
Configuratie RSA key

skill(config)#crypto key generate rsa


The name for the keys will be: skill.skill.local

Choose the size of the key modulus in the range of 360 to 2048 for your

General Purpose Keys. Choosing a key modulus greater than 512 may take

a few minutes.

  

How many bits in the modulus [512]: 2048

% Generating 2048 bit RSA keys, keys will be non-exportable...[OK]
```

```
Configuratie VTY 

Switch(config)#line vty 0 3
Switch(config-line)#password Str0ng3rP@55w0rd
Switch(config-line)#exit
```

> [!warning] >
Schakel niet gebruikte switch poorten uit en plaats deze in vlan 1000'

> [!info] >
>gebruikte poorten 
>Fa 0/1 - 2 voor desktop
>Fa 0/24 voor DHCP
> 

```
Configuratie vlan 1000:

skill(config)#vlan 1000
skill(config-vlan)#name 1000
```

```
Configuratie niet gebruikte switchporten:

skill(config)#interface range fastEthernet 0/3 - 23
skill(config-if-range)#shutdown
skill(config-if-range)#switchport access vlan 1000
skill(config-if-range)#exit
```

> [!warning] >
> Vlan hopping
> Beveilig de trunk poorten van de switch voor vlan hopping 
>

```
Configuratie antie VLAN hopping:

skill(config)#interface range gigabitEthernet 0/1 - 2
skill(config-if)#switchport trunk encapsulation dot1q
skill(config-if)#switchport mode trunk
skill(config-if)#switch port nonegotiate
```

> [!warning] >
> Migrate DHCP attach
> voorkom dat andere DHCP server op het netwerk IP addressen uitdelen  

> [!info] >
DHCP server bevind zich op Fa /024

```
Configuratie dhcp snooping

skill(config)#interface fastEthernet 0/24
skill(config-if)#ip dhcp snooping trust
```
