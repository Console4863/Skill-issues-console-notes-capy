tags: #leren #school #friesepoort #project-security
links: https://systemzone.net/ubuntu-radius-server-configuration-with-freeradius/

--- 
## Installatie Radius

Stap 1: Update je systeem Open een terminalvenster en voer de volgende commando's uit om ervoor te zorgen dat je systeem up-to-date is:

sql

`sudo apt update sudo apt upgrade`

Stap 2: Installeer FreeRADIUS FreeRADIUS is een populaire open-source RADIUS-server. Gebruik het volgende commando om FreeRADIUS te installeren:

`sudo apt install freeradius`

Stap 3: Configureer FreeRADIUS Navigeer naar de configuratiemap van FreeRADIUS met het volgende commando:

`cd /etc/freeradius/3.0/`

Open het bestand `radiusd.conf` in een teksteditor, zoals Nano:


`sudo nano radiusd.conf`

Zoek de sectie "security" in het bestand en zoek naar de lijn `allow = 127.0.0.0/24`. Verander deze naar `allow = 0.0.0.0/0` om alle IP-adressen toe te staan verbinding te maken met de RADIUS-server.

Sla het bestand op en sluit de teksteditor af.

Stap 4: Start de RADIUS-server Start de RADIUS-server met het volgende commando:

`sudo systemctl start freeradius`

Je RADIUS-server is nu actief en kan verzoeken verwerken.

Stap 5: Test je RADIUS-server Om te controleren of je RADIUS-server correct is geïnstalleerd en werkt, kun je de volgende opdracht gebruiken om een verificatietest uit te voeren:

`radtest <gebruikersnaam> <wachtwoord> localhost 0 testing123`

Vervang `<gebruikersnaam>` en `<wachtwoord>` door de gewenste referenties voor je RADIUS-gebruiker.

Als de test slaagt, ontvang je een bericht dat de verificatie is geslaagd. Dit betekent dat je RADIUS-server correct werkt.

Dat is alles! Je hebt nu succesvol een RADIUS-server geïnstalleerd op je Ubuntu-server. Vergeet niet om de server naar behoefte verder te configureren, zoals het toevoegen van gebruikers, het instellen van beveiligingsopties en het configureren van netwerktoegangsbeleid. Raadpleeg de documentatie van FreeRADIUS voor meer informatie over configuratie-opties en mogelijkheden.

Om een gebruiker te configureren in de FreeRADIUS-server, volg je de onderstaande stappen:

## Gebruiker toevoegen aan Radius

Stap 1: Open het configuratiebestand Navigeer naar de configuratiemap van FreeRADIUS met het volgende commando:


`cd /etc/freeradius/3.0/`

Open het bestand `users` in een teksteditor, zoals Nano:


`sudo nano users`

Stap 2: Voeg de gebruikersinformatie toe In het `users`-bestand kun je gebruikersconfiguraties toevoegen. Elke gebruiker wordt gedefinieerd op een aparte regel met het volgende formaat:


`<gebruikersnaam> Cleartext-Password := "<wachtwoord>"`

Vervang `<gebruikersnaam>` door de gewenste gebruikersnaam en `<wachtwoord>` door het wachtwoord voor die gebruiker. Het wachtwoord moet tussen aanhalingstekens worden geplaatst.

Hier is een voorbeeldconfiguratie voor een gebruiker met de gebruikersnaam "vogel" en het wachtwoord "FPitDr88":


`vogel Cleartext-Password := "FPitDr88"`

Stap 3: Sla het bestand op Sla het `users`-bestand op en sluit de teksteditor af.

Stap 4: Herstart de RADIUS-server Herstart de RADIUS-server met het volgende commando om de wijzigingen toe te passen:

`sudo systemctl restart freeradius`

De gebruiker "vogel" is nu geconfigureerd in de RADIUS-server met het opgegeven wachtwoord.

Je kunt deze stappen herhalen om andere gebruikers toe te voegen of om de configuratie van bestaande gebruikers bij te werken. Vergeet niet de RADIUS-server opnieuw te starten telkens wanneer je wijzigingen aanbrengt in het `users`-bestand..

## Client toevoegen aan radius

Om je TP-Link router te laten authenticeren op de RADIUS-server, moet je de volgende stappen volgen:

Stap 1: Maak een RADIUS-client op de RADIUS-server Op de RADIUS-server moet je een configuratie maken voor de TP-Link router als RADIUS-client. Dit om de router te identificeren en te autoriseren om verbinding te maken met de RADIUS-server.

1. Navigeer naar de configuratiemap van FreeRADIUS:

bashCopy code

`cd /etc/freeradius/3.0/`

2. Open het bestand `clients.conf` in een teksteditor:

Copy code

`sudo nano clients.conf`

3. Voeg een nieuwe sectie toe voor de TP-Link router met de volgende informatie (voorbeeldconfiguratie):

```
client tp-link-router {
    ipaddr = 192.168.1.1
    secret = sharedsecret
    require_message_authenticator = no
    nas_type = other
    shortname = tp-link-router
}
```