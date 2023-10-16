
![[Pasted image 20231004115227.png]]

![[OpdrACLs.doc]]

1. Blokkeer het verkeer van Berlijn naar Amsterdam

Configuratie gedaan in router van Amsterdam

```
Router (config)#access-list 10 deny 200.4.4.0 0.0.0.255

Router (config)#access-list 10 permit any

Router (config)#int S0

Router (config_if)#IP access-group 10 in
```

![[Pasted image 20231004115300.png]]

![[Pasted image 20231004115306.png]]

1. Host met een oneven IP vanaf Parijs naar London worden geblokkeerd.

```
Router(config)# access-list 10 deny 200.1.1.1 0.0.0.254

Router(config)# access-list 10 permit any

Router(config)# interface Serial0

Router(config-if)# ip access-group 10 in
```

Host met een even ip:

![[Pasted image 20231004115324.png]]

Host met een oneven ip:

![[Pasted image 20231004115333.png]]

1. Host met een even IP van Parijs naar Londen worden geblokkeerd.

```
Router(config)# access-list 10 deny 200.1.1.0 0.0.0.254

Router(config)# access-list 10 permit any

Router(config)# interface Serial0

Router(config-if)# ip access-group 10 in
```

Pc met een even ip:

![[Pasted image 20231004115425.png]]

Pc met een oneven IP:

![[Pasted image 20231004115447.png]]

1. Van Parijs naar Berlijn worden alle host met een IP lager dan 128 geblokkeerd.

```
Router(config)# access-list 10 deny 200.1.1.0 0.0.0.127

Router(config)# access-list 10 permit any

Router(config)# interface gigabit 0/0

Router(config-if)# ip access-group 10 out
```

1. Blokkeer de host met een IP adres van 64 tot en met 127 van Amsterdam naar Berlijn.  
     

```
Router(config)# access-list 10 deny 200.5.5.64 0.0.0.63

Router(config)# access-list 10 permit any

Router(config)# interface gigabit 0/0

Router(config-if)# ip access-group 10 out
```

1. Blokkeer de host met een IP adres van 128 tot en met 159 van Parijs naar London.

```
Router(config)# access-list 10 deny 128.0.0.0 0.0.0.31

Router(config)# access-list 10 permit any

Router(config)# interface GigabitEthernet0/0

Router(config-if)# ip access-group 10 out
```

1. Configureer de router van Berlijn zodat van afstand met telnet de router kan worden geconfigureerd.

```
Router(config)# line vty 0 4

Router(config-line)# password cisco

Router(config-line)# login

Router(config-line)# transport input telnet

Router(config-line)# exit

Router(config)# ip telnet server
```
 

1. Zorg ervoor dat alleen uit het netwerk van Berlijn de router van Berlijn kan worden geconfigureerd.

```
Router(config)# access-list 10 permit 200.4.4.0 0.0.0.255

Router(config)# access-list 10 deny any

Router(config)# line vty 0 4

Router(config-line)# access-class 10 in

Router(config-line)# exit
```

1. Hoe kun je in één regel de IP adressen 64 en 65 van Parijs naar Berlijn blokkeren?

```
Router(config)# access-list 10 deny host 200.1.1.64

Router(config)# access-list 10 deny host 200.1.1.65

Router(config)# access-list 10 permit any

Router(config)# interface GigabitEthernet0/0

Router(config-if)# ip access-group 10 out
```

1. Hoe kun je in één regel de IP adressen 80 en 81 van London naar Berlijn blokkeren?

```
Router(config)# access-list 10 deny host 200.2.2.80 0.0.0.1

Router(config)# access-list 10 permit any

Router(config)# interface GigabitEthernet0/0

Router(config-if)# ip access-group 10 out
```