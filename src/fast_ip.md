# Sette fast IP-adresse

## Sette fast IP basert på MAC-adresse

Det anbefales at IP-adressen settes av DHCP-serveren i nettverket ved å reservere en IP-adresse basert på MAC-adressen til AC5000. Dette gjøres i DHCP-serverens konfigurasjon. MAC-adressen til AC5000 finnes på etiketten på siden av enheten, samt på info-fanen på skjermen. 

Etter at IP-adressen er reservert, startes AC5000 på nytt for å få tildelt den faste IP-adressen.

## Sette en statisk IP ved bruk av /etc/dhcpcd.conf

Dersom det ikke er mulig å sette fast IP-adresse i DHCP-serveren, kan en statisk IP-adresse settes direkte på AC5000. Dette gjøres ved å redigere konfigurasjonsfilen `/etc/dhcpcd.conf`.

For å konfigurere en statisk IP-adresse på AC5000 må du logge inn via SSH ved hjelp av et program som PuTTY eller en tilsvarende SSH-klient.

### Steg 1: Logg inn på systemet

1. Åpne SSH-klientprogram.
2. Koble PC til LAN2-porten på AC5000.
3. Skriv inn IP-adressen 192.168.0.10 i feltet for "Host Name (or IP address)".
4. Sørg for at porten er satt til `22` (standard for SSH).
5. Klikk på "Open" for å starte en SSH-økt.
6. Når du blir bedt om det, logg inn med brukernavnet `user` og passordet `AiwellAC5000`.

### Steg 2: Åpne dhcpcd-konfigurasjonsfilen

1. Etter at du har logget inn, åpne filen `/etc/dhcpcd.conf` ved å bruke en teksteditor. For eksempel, for å bruke nano, skriv:

   ```
   sudo nano /etc/dhcpcd.conf
   ```

2. Du kan bli bedt om å skrive inn passordet ditt igjen.

### Steg 3: Konfigurer en statisk IP-adresse for LAN1 (eth0)

1. Gå ned med piltaster til du finner innstillinger for `interface eth0`. Hvis det allerede finnes en seksjon for fallback, som `profile static_eth0` eller lignende, kan du enten redigere denne eller legge til en ny konfigurasjon for `eth0`.
2. For å sette en statisk IP-adresse, legg til eller endre følgende linjer under `interface eth0`. Erstatt `<statisk-ip>`, `<gateway-ip>`, og `<dns-ip>` med dine faktiske verdier:

   ```
   interface eth0
   static ip_address=<statisk-ip>/24
   static routers=<gateway-ip>
   static domain_name_servers=<dns-ip>
   ```

   Eksempel:

   ```
   interface eth0
   static ip_address=192.168.1.100/24
   static routers=192.168.1.1
   static domain_name_servers=8.8.8.8 8.8.4.4
   ```

   `/24` etter IP-adressen angir subnettmasken. Dette er den vanligste subnettmasken, og tilsvarer 255.255.255.0 på Windows. Hvis du er usikker, kan du sjekke nettverksinnstillingene på en annen enhet som er koblet til samme nettverk, eventuelt kontakte IT-avdelignen som tildelte IP-adressen.

   `static domain_name_servers` angir DNS-servere. Dette er valgfritt, men nødvendig dersom du vil at AC5000 skal kunne kommunisere med eksterne servere via domenenavn som er tilfellet ved oppdateringer og bruk av værprognoser fra Meterologisk Institutt til styring. Hvis du er usikker, kan du bruke Googles DNS-servere som i eksempelet over.

   **Viktig:** Sørg for at du kun redigerer innstillinger for `eth0` (LAN1).

### Steg 4: Lagre endringene og start nettverkstjenesten på nytt

1. Lagre endringene og lukk teksteditoren. Hvis du bruker nano som teksteditor, gjør du dette ved å trykke `Ctrl+X`, deretter `Y` for å bekrefte lagring, og til slutt `Enter` for å lukke.
2. For å aktivere de nye nettverksinnstillingene, start enten nettverkstjenesten eller AC5000 på nytt. For å restarte nettverkstjenesten, skriv:
   ```
   sudo service dhcpcd restart
   ```
   Alternativt kan du restarte AC5000 ved å skrive:
   ```
   sudo reboot
   ```

Etter at systemet har startet på nytt, vil AC5000 bruke den statiske IP-adressen du har konfigurert for LAN1 (eth0).
