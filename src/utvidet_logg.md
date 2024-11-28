# Utvidet logg

AC5000 har begrenset lagringskapasitet for loggdata. For å unngå at loggdata slettes, kan Aiwell tilby en ekstern loggserver som lagrer loggdata fra AC5000. Dette kan være nyttig for å overvåke og analysere data over lengre tid, for eksempel for å optimalisere regulering eller for å dokumentere driften.

Normal driftslogg er hovedsaklig hendelsesbasert, det vil si at den lagrer data om endringer i systemet, for eksempel når systemet starter eller stopper, eller når det utløses en alarm. Utvidet logg kan lagre data med høyere oppløsning, for eksempel temperaturer og pådrag, og kan også lagre data over lengre tid.

Ekstern loggserver er spesielt anbefalt i prosjekter der AC5000 ikke er tilknyttet et SD-anlegg, eller der det er behov for bistand fra Aiwell for å overvåke og analysere data.

AC5000 kommuniserer med loggserveren via MQTT. Nettverket må derfor ha tilgang til internett, og brannmuren må tillate utgående trafikk over port 1883.
