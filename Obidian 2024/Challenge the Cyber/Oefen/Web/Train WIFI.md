> [!INFO] >
> web
> 

tags: #CTF #hacken [[CTF]]

```
## TrainWifi - 1
CTF{always_check_your_sources}

Oplossing:

Bekijk de HTML code de vlag staat onder aan
```

![[Pasted image 20230412194923.png]]

```
## TrainWifi - 2
CTF{train_inspection_passed} 

Oplossing:

Doe rechter muis knop op de knop Request WI-FI code en klik op en inspect vervang vervolgens:
<button class="btn btn-primary" disabled="">Request Wi-Fi code</button>

Met:
<button class="btn btn-primary" enable="">Request Wi-Fi code</button>

Hierna kan je de knop indrukken en word de vlag zichtbaar
```

![[Pasted image 20230412195202.png]]

![[Pasted image 20230412194325.png]]

> [!WARNING] >
> Voor de volgende opdracht is Burp Suite gebruikt
> 

```
## TrainWifi - 3
CTF{i_know_how_to_read_websockets}

Oplossing:

Open Burp suite en kijk in het tablad Proxy.
Zet vervolgens Intercept aan.
Zoek vervolgens de gewenste webpagina op.
De Flag komt in plain tekst te staan.
```

![[Pasted image 20230509151857.png]]