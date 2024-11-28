# Fjerntilgang

Dersom Aiwell skal kunne tilby bistand under igangkjøring og prøvedrift, er det nødvendig med fjerntilgang til AC5000. Dette gjør det mulig for Aiwell å koble seg til AC5000 via internett for å feilsøke og konfigurere enheten. Fjerntilgang kan også være nyttig for kunden, for eksempel for å hente ut logger og konfigurere enheten.

Aiwell kan levere en ferdig konfigurert enhet med kryptert fjerntilgang via mobil-modem, eller tilgang kan settes opp av kunden selv.

Det er stor variasjon i nettverksoppsett og sikkerhetsinnstillinger, og det er derfor ikke mulig å gi en generell oppskrift på hvordan fjerntilgang settes opp i henhold til de interne regler of føringer som gjelder i kundens nettverk. I de aller fleste tilfeller dekkes minstekavene av standardinnstillinger i kundens nett, men det kan være nødvendig å gjøre tilpasninger i brannmur eller rutere. Det bør bekreftes at følgene krav er oppfylt:

**SSH:** Fjerntilgang til AC5000 skjer via SSH (Secure Shell) over port 22. Dette betyr at port 22 må være åpen for inngående trafikk til AC5000.

**HTTP/HTTPS:** Standardportene 443/80 for web-grensesnittet må være riktig videresendt. Aiwell anbefaler at det brukes HTTPS (port 443) for å sikre at all trafikk er kryptert, men nettverks-administrator må selv bestille et SSL-sertifikat for å bruke HTTPS. Aiwell kan installere sertifikatet på enheten.

**WebSockets:** Web-grensesnittet bruker WebSocket-tilkoblinger for å kommunisere. Brannmuren må tillate WebSocket-trafikk over samme port 443/80.

**Stateful Inspection:** Brannmuren bør støtte "stateful packet inspection" (SPI) for å tillate returtrafikk av en etablert tilkobling.

**Ingen begrensninger på Payload-størrelse:** Sørg for at det ikke er noen restriksjoner på størrelsen på nyttelasten for HTTP POST-forespørsler, som er hvordan web-grensesnittet gjør utrullinger.

**Application Layer Gateway (ALG):** Hvis brannmuren bruker en ALG-funksjon for HTTP, bør den konfigureres eller deaktiveres da den noen ganger kan forstyrre WebSocket-trafikk.

**Cross-Site Request Forgery (CSRF) Beskyttelser:** Hvis brannmuren har beskyttelser mot CSRF, må den konfigureres for å gjenkjenne og akseptere forespørsler fra web-grensesnittets editor.