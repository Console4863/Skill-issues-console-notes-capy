> [!INFO] >
> Uitwerking Flag Store

tags: #CTF #hacken [[CTF]]

Opdracht:

![[Pasted image 20230508190313.png]]

Uitwerking:

```
Stap 1:
Vul iets randoms in in de zoekbalk van de website. Klik vervolgens op Search
```

![[Pasted image 20230508190609.png]]

```
Stap 2:
Open het cookie menu van de browser. Daar staan vervolgens 2 cookies. Last-search en session. Bijde zijn versleuteld in een base64. 
```

![[Pasted image 20230508190716.png]]
```
Stap 3:
Kopieer de value van de session in de value van de last search en ververs vervolgens de pagina. Hierna komt het volgende in de zoek balk te staan:

{"flag-credit": 0, "log-id": "6073974ae4655e6c"}
```

```
Stap 4:
Verander de string naar het volgende:

{"flag-credit": 5000, "log-id": "6073974ae4655e6c"}

Druk vervolgens op search.
```

```
Stap 5:
Ga terug naar de cookie instellingen en vul de Value van last-search in bij session ververs vervolgens de pagina. Nu zou je 5000 credit moeten hebben.
```

![[Pasted image 20230508191414.png]]

```
Stap 6:
Het kopen van de flag zoek naar de volag met de onderstaande afbeelding en druk vervolgens op kopen
```

![[Pasted image 20230508191510.png]]

```
Stap 7:
De flag is nu zicht baar bij het order nummer de flag voor CTF is:

CTF{6kfq8sbwa7}
```

![[Pasted image 20230508191638.png]]