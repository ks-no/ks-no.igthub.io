---
title: Folkeregister
date: 2020-11-19
---

## Fiks folkeregister

KS vil tilby det nye Folkeregisteret(FREG) via Fiks-plattformen for kommunal sektor, foruten helse. E-helse tilbyr løsning for den delen som omhandler helse.

Fiks folkeregister er en tjeneste som tilbyr maskin-til-maskin integrasjon for å hente ut data fra Folkeregisteret. Fiks folkeregister tilbyr et proxy-api som gjør det mulig for leverandører å bruke skatteetatens api-er for dette formålet.
Fiks folkeregister bruker "roller" som sørger for riktig tilgangsstyring ved bruk av proxy-api-et.

Skatteetatens [api-dokumentasjon](https://skatteetaten.github.io/folkeregisteret-api-dokumentasjon/om-tjenestene/) for Folkeregisteret er også relevant for bruk av proxy-api-et.

Mer informasjon om Fiks folkeregister finner man [her](https://www.ks.no/fagomrader/digitalisering/utviklingsprosjekter/modernisert-folkeregister).

## Hvordan tar man i bruk Fiks folkeregister?

Før man kan ta i bruk Fiks folkeregister må kommunen inngå avtaler og tildele KS rettigheter i Altinn. Dette er beskrevet [her](https://portal.fiks.ks.no/fiks/fiks-folkeregister/).
 
Kommunen må deretter konfigurere opp [rolle(r)](https://ks-no.github.io/fiks-plattform/modernisert-folkeregister/#roller) og [integrasjon](https://ks-no.github.io/fiks-plattform/modernisert-folkeregister/#integrasjonsutvikling) i Fiks Konfigurasjon som fagsystem-leverandøren trenger for å bruke api-ene.
 
### Roller
For å bruke proxy-api-et til Fiks trenger man å definere roller som brukes for tilgangsstyring. 
En rolle blir brukt for å begrense opplysninger som kan hentes ut fra Folkeregisteret. Alle forespørsler, både for personer og integrasjoner, må gjøres i kontekst av en rolle. 

En rolle inneholder begrensninger for hvilke hjemler som er tillatt, hvilke bruksområder den skal brukes til og hvilke felter som er tillatt å hente ut fra Folkeregisteret.
Kommunen oppretter en eller flere roller i Fiks Konfigurasjon. Der må man også tildele tilgang til en integrasjon for bruk av rollen, som fagsystemet kan bruke mot proxy-api-et. 
Man får også oppgitt en tilhørende rolle-id, som fagsystemet må spesifisere i URL-pathen mot proxy-api-et.

### Integrasjonsutvikling

Informasjon om generell integrasjonsutvikling mot Fiks, som blant annet autentisering, finner man [her](https://ks-no.github.io/fiks-plattform/integrasjoner/). For Fiks folkeregister skal det brukes "integrasjon".

API-kall gjøres i henhold til [skatteetatens API-er](https://app.swaggerhub.com/organizations/Skatteetaten_FREG), hvor både offentlig med hjemmel og offentlig uten hjemmel kan brukes. 
Det er likevel noen endringer som må gjøres, for hvordan URL-stien er bygd opp.

URL-sti for Fiks sitt proxy-api er på formen:
```/folkeregister/api/v1/{rolleId}/{skatteetatenRessurs}```

- ```rolleId``` - Id for rollen som brukes
- ```skatteetatenRessurs``` - URL-sti for oppslag/uttrekk/hendelser fra skatteetatens api, på formen med eksempel ```v1/personer/{personidentifikator}```

Merk at dette er URL-stien som skal brukes uavhengig av om fagsystemet bruker api for offentlig med hjemmel eller offentlig uten hjemmel, da det er rollen som definerer hvilken som blir brukt.  

API-endepunkter: \
Test: ```https://api.fiks.test.ks.no/folkeregister/api/v1/{rolleId}/{skatteetatenRessurs}``` \
Prod: ```https://api.fiks.ks.no/folkeregister/api/v1/{rolleId}/{skatteetatenRessurs}```


### Kontakt
Spørsmål og henvendelser vedrørende modernisert folkeregister kan rettes til modernisertfolkeregister@ks.no