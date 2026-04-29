Hei,   
  
Kan vi ta en prat rundt hvordan vi bruker miljøene våre I dag og forbedringspotensiale? 

**Mål med møtet er å få svar på følgende spørsmål:** 
1. Skal vi gjøre noen forbedringer mtp. denne tematikken nå?
2. Isåfall, hvilke forbedringer?
3. Skal det gjøres stegvis eller samtidig?

  

Uheldige brukermønstre jeg ønsker å pirke borti er:

- Utvikling I prod
- Lite bruk av test-miljøet
- Forskjell på hva som finnes av data etc. I de forskjellige miljøene

  

Sånn konkret så er et forslag noe i form av: 

- Prod-data I alle miljø
- Read-only i prod (og test?)
- Utvikling mot en branch (GitHub Flow vs Git Flow)
- Skille deployment til test og prod (slik at vi i større grad oppdager bugs i test og ikke prod)

  

Andre ting som kan være relevant/nyttig

- Prod i alle miljø betyr fort prod-mengde med data

- (er dette ok? Kan vi løse det på noe vis? Hva er alternativet?)

- Databricks asset bundles (DAB)
- Kritikalitet ref. Nytt workspace etc. 
- Hvor mye arbeid er det?
- Kildesystemer som har forskjellige miljøer med forskjellig data
- Mer kontinuerlig arbeidsflyt vil bety et større behov for tester
- Mimirflow  som en del av deployment-pakken og ikke som en egen fil som må legges til på cluster
- Og helt sikkert masse annet lurt som dere kommer på 🙂