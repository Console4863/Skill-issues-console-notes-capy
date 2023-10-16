> [!INFO] >
> forensics
> 

tags: #CTF #hacken [[CTF]]

```
## Holmes' Journey: Analysis #1
CTF{G3v0nden_h1dd3n_t3kstje_v33l_m33_t0ch}

Oplossing:

Open de foto met notepadd++ of andere HEX editor
Flag is vervolgens te vinden op het einde van line 704
```

![[Pasted image 20230412194804.png]]

```
## Holmes' Journey: Analysis #2
CTF {You_are_a_Sherlock_g03d_man}

Oplossing:

Gebruikte commando's:

apt install eog
binwalk Holmes2.jpg
binwalk --dd=.* Holmes2.jpg
cd _Holmes2.jpg-0.extracted
eog 9E0
```

![[Pasted image 20230412130704.png]]

```
## Holmes' Journey: Analysis #3
CTF{G3n1us_13v31_st3g0_h3r0}

Oplossing:

Een afbeelding begint altijd in HEX met een FF D8 en eindigt met een FF D9. De afbeelding moest worden geopend met een HEX editor aangezien er nog een tussen afbeelding in de afbeelding zelf zat. Deze afbeelding moest worden verwijderd dus alle data tussen de 2e FF D8 en FF D9 moest worden verwijdered daarna werd de afbeelding goed zichtbaar
```

![[test.jpg]]