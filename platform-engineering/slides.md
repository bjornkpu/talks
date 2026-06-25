---
title: 'Hvorfor Platform Engineering'
description: 'Skaler utviklingsorganisasjonen — ikke kompleksiteten. Introduksjon til Platform Engineering og Internal Developer Platforms (IDPs): hvorfor golden paths og selvbetjening gir utviklerverdi, hva det betyr for utviklere, ops og virksomheten, og hvordan man starter med en Minimum Viable Platform.'
author: 'Bjørn Kristian Punsvik'
keywords: ['platform engineering', 'internal developer platform', 'IDP', 'golden paths', 'developer experience', 'DevEx', 'DevOps', 'SRE', 'platform as a product', 'team topologies', 'selvbetjening', 'developer productivity']
marp: true
theme: hvorfor-platform-engineering
paginate: true
html: true
transition: fade 0.2s
---

<script type="module">
  import mermaid from "https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs";
  mermaid.initialize({
    startOnLoad: true,
    theme: "base",
    flowchart: { htmlLabels: false, nodeSpacing: 40, rankSpacing: 60, padding: 16 },
    themeVariables: {
      fontFamily: "Inter, system-ui, -apple-system, 'Segoe UI', sans-serif",
      fontSize: "18px",
      primaryColor: "#1b3d46",
      primaryTextColor: "#ffffff",
      primaryBorderColor: "#f96c4f",
      lineColor: "#a0b0b8",
      tertiaryColor: "#f96c4f"
    }
  });
</script>

<!-- _class: lead -->
<!-- _paginate: false -->
<!-- _header: '' -->

![hero fade](../assets/images/121-GettyImages-1254770264.jpg)

# Platform Engineering

Internal Developer Platform

<div class="byline">

Bjørn Kristian Punsvik

2026-05-03

</div>

<!-- Notat:

[REGI]
- la tittelen puste — ikke begynn rett på
- 2-3 sek stillhet før første ord

[STIKKORD]
- kort velkomst

-->

---

<!-- _class: hook -->
<!-- _paginate: false -->
<!-- _header: '' -->
<!-- _footer: '' -->
<!-- _transition: 'fade 1s' -->


# Utviklerne deres er av de dyreste ressursene dere har. Hva gjør de når de <span class="morph-gap">ikke skriver kode</span>?

<!-- Notat:

[REGI]
- spørsmålet skal henge — ikke svar

[STIKKORD]

[BRO]
- klikk uten ord

-->

---

<!-- _class: hook -->
<!-- _paginate: false -->
<!-- _header: '' -->
<!-- _footer: '' -->
<!-- _transition: 'fade 1s' -->


# De beste ops-folkene dine <span class="morph-gap">svarer på tickets</span>. De løser ikke arkitektur.

<!-- Notat:

[REGI]
- spørsmålet skal henge — ikke svar

[STIKKORD]

[BRO]
- pause, klikk

-->

---

<!-- _class: hook -->
<!-- _paginate: false -->
<!-- _header: '' -->
<!-- _footer: '' -->
<!-- _transition: 'fade 1s' -->


# De beste utviklerne dine bygger ikke produkt. De <span class="morph-gap">vedlikeholder infrastruktur</span>.

<!-- Notat:

[REGI]
- spørsmålet skal henge — ikke svar

[STIKKORD]


[BRO]
- klikk inn i bio — du tar over scenen

-->

---

<!-- _footer: '' -->
<!-- _header: '' -->
<!-- _paginate: false -->

<div class="neofetch">

<img src="../assets/images/profile.jpg" alt="Bjørn Kristian Punsvik">

<pre><span class="prompt">bk@softwareone:~$</span> <span class="cmd">whoami</span>
<span class="rule">--------------------</span>
<span class="key">Name</span>:       <span class="morph-gap">Bjørn Kristian Punsvik</span>
<span class="key">Role</span>:       Data & Software Engineer
<span class="key">Position</span>:   Senior Consultant
<span class="key">Location</span>:   Trondheim
<span class="key">Uptime</span>:     30 years
<span class="key">Experience</span>: 6 years
<span class="key">Education</span>:  B.Sc. Computer Engineering, NTNU

<span class="prompt">bk@softwareone:~$</span> <span class="cmd">ps -a</span>
<span class="rule">--------------------</span>
<span class="key">START    DURATION  PROJECT</span>
2017-08  3y        /ntnu/tihlde-drift
2020-07  2y 3m     /enoco/eurora-cloud
2023-06  1y 6m     /equinor/grc
2024-12  3m        /equinor/fos
2025-09  →         /enova/mimir
2026-03  →         /enova/ai
</pre>

</div>

<!-- Notat:

[REGI]
- ~50 sek total
- rolig tempo — autentisitet før autoritet
- beats: navn (5s) → origin (12s) → credentials (25s) → bro (8s)
- la tittelen "whoami" puste

[STIKKORD]
- NAVN: Bjørn, SoftwareOne, for tiden hos Enova
- ORIGIN:
NTNU + TIHLDE Drift, hjemme-cluster, klassisk trent som software utvikler, men trives godt mot infra. som trives mot infra
- CREDENTIALS:
Profesjonelt har jeg vært tech lead på en skybasert energiplattform hos Enoco, jobbet med integrasjonsplattform hos Equinor, og står nå i to team hos Enova — produkt og dataplattform — med moderniseringsprogrammet på siden.

Jeg ser hverdagen fra flere vinkler.

- BRO:
Og det jeg ser igjen og igjen, kostnaden ved manglende plattform er ikke teknisk gjeld. Det er at de beste utviklerne stopper å bygge nytt og begynner å vedlikeholde sin egen versjon av infrastrukturen. Det er det vi skal snakke om i dag.

[POENG]
- "jeg ser hverdagen fra flere vinkler" — kort, ikke selg
- bro skal lande direkte i diagnose-fasen

[BRO]
- "det er det vi skal snakke om i dag" → klikk

-->

---

# Slik ser det ut når den ikke er bygget med vilje

![chaos](svg/chaos-10-stacks.svg)

Ti team. Ti stacker. Ti måter å gjøre det samme på. Ett security-team som forsøker å se på tvers — uten en sjanse.

<!-- Notat:

[REGI]
- diagnose-fasen åpner
- pek på diagrammet — la det jobbe
- ikke teknisk dybde, fokuser på mønsteret

[STIKKORD]
- hver boks = ett team som måtte bygge selv
- ikke fordi de ville — fordi alternativet var ingen plattform
- ti versjoner av samme fundament, ti måter å misforstå sikkerhet på
- security-boksen: ingen sjanse til å håndheve compliance på ti stacker
- "dette er hva 'vi har en plattform' ofte betyr i praksis"

[POENG]
- treffer CTO-personaen direkte — dette er kostnaden av tilfeldighet

[BRO]
- "men ikke bare på org-nivå — også per utvikler" → kognitiv last

-->

---

<!-- _transition: 'fade 1s' -->


# Cloud-native ble for mye for ett menneske

<div class="cognitive-load">
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1100 480" font-family="Arial, Helvetica, sans-serif" style="width:100%; height:auto;">
  <defs>
    <style>
      .pill { stroke-width: 1.2; fill: rgba(255,255,255,0.05); stroke: rgba(255,255,255,0.25); }
      .pill-hot { fill: rgba(247,103,94,0.18); stroke: #F7675E; }
      .pill-text { fill: #FFFFFF; font-weight: 600; }
      .person { fill: #FFFFFF; }
      .body { fill: none; stroke: #FFFFFF; stroke-width: 2; stroke-linecap: round; }
      .crush-line { stroke: #F7675E; stroke-width: 1.5; opacity: 0.5; fill: none; stroke-linecap: round; }
      .label { fill: #A1A7AE; font-size: 13px; font-style: italic; }
      .small-line { stroke: rgba(255,255,255,0.3); stroke-width: 1; fill: none; }
    </style>
  </defs>
  <g font-size="16">
    <rect class="pill" x="320" y="100" width="92" height="30" rx="15"/>
    <text class="pill-text" x="366" y="120" text-anchor="middle" font-size="13">GitOps</text>
    <rect class="pill" x="430" y="105" width="100" height="30" rx="15"/>
    <text class="pill-text" x="480" y="125" text-anchor="middle" font-size="13">Argo CD</text>
    <rect class="pill" x="650" y="105" width="100" height="30" rx="15"/>
    <text class="pill-text" x="700" y="125" text-anchor="middle" font-size="13">Istio</text>
    <rect class="pill" x="770" y="100" width="120" height="30" rx="15"/>
    <text class="pill-text" x="830" y="120" text-anchor="middle" font-size="13">Prometheus</text>
    <rect class="pill" x="220" y="155" width="100" height="28" rx="14"/>
    <text class="pill-text" x="270" y="174" text-anchor="middle" font-size="12">CRDs</text>
    <rect class="pill" x="480" y="155" width="120" height="28" rx="14"/>
    <text class="pill-text" x="540" y="174" text-anchor="middle" font-size="12">CI pipelines</text>
    <rect class="pill" x="620" y="160" width="100" height="28" rx="14"/>
    <text class="pill-text" x="670" y="179" text-anchor="middle" font-size="12">Crossplane</text>
    <rect class="pill" x="740" y="155" width="100" height="28" rx="14"/>
    <text class="pill-text" x="790" y="174" text-anchor="middle" font-size="12">OPA</text>
    <rect class="pill" x="860" y="160" width="120" height="28" rx="14"/>
    <text class="pill-text" x="920" y="179" text-anchor="middle" font-size="12">OpenTelemetry</text>
    <rect class="pill" x="180" y="210" width="80" height="26" rx="13"/>
    <text class="pill-text" x="220" y="227" text-anchor="middle" font-size="11">Backstage</text>
    <rect class="pill" x="280" y="215" width="80" height="26" rx="13"/>
    <text class="pill-text" x="320" y="232" text-anchor="middle" font-size="11">Grafana</text>
    <rect class="pill" x="380" y="210" width="100" height="26" rx="13"/>
    <text class="pill-text" x="430" y="227" text-anchor="middle" font-size="11">SealedSecrets</text>
    <rect class="pill" x="500" y="215" width="80" height="26" rx="13"/>
    <text class="pill-text" x="540" y="232" text-anchor="middle" font-size="11">Service Mesh</text>
    <rect class="pill" x="600" y="210" width="80" height="26" rx="13"/>
    <text class="pill-text" x="640" y="227" text-anchor="middle" font-size="11">Loki</text>
    <rect class="pill" x="700" y="215" width="80" height="26" rx="13"/>
    <text class="pill-text" x="740" y="232" text-anchor="middle" font-size="11">Tekton</text>
    <rect class="pill" x="800" y="210" width="100" height="26" rx="13"/>
    <text class="pill-text" x="850" y="227" text-anchor="middle" font-size="11">Cert-Manager</text>
    <rect class="pill" x="920" y="215" width="80" height="26" rx="13"/>
    <text class="pill-text" x="960" y="232" text-anchor="middle" font-size="11">Falco</text>
    <rect class="pill" x="100" y="125" width="80" height="26" rx="13"/>
    <text class="pill-text" x="140" y="142" text-anchor="middle" font-size="11">Containerd</text>
    <rect class="pill" x="900" y="60" width="100" height="28" rx="14"/>
    <text class="pill-text" x="950" y="78" text-anchor="middle" font-size="12">CNI / CSI</text>
  </g>
  <path class="crush-line" d="M 440 250 L 520 320"/>
  <path class="crush-line" d="M 530 250 L 540 320"/>
  <path class="crush-line" d="M 620 250 L 560 320"/>
  <path class="crush-line" d="M 700 250 L 580 320"/>
  <path class="crush-line" d="M 360 250 L 510 320"/>
  <g transform="translate(540,330)">
    <circle class="person" cx="0" cy="0" r="14"/>
    <path class="body" d="M -2 14 L -2 60"/>
    <path class="body" d="M -2 30 L -25 55"/>
    <path class="body" d="M -2 30 L 21 55"/>
    <path class="body" d="M -2 60 L -16 95"/>
    <path class="body" d="M -2 60 L 12 95"/>
  </g>
  <text class="label" x="550" y="450" text-anchor="middle" font-size="14">Hver utvikler forventes å mestre alt dette — i tillegg til å levere produkt.</text>
</svg>
<div class="tool-pill k8s">Kubernetes</div>
<div class="tool-pill tf">Terraform</div>
<div class="tool-pill helm">Helm</div>
<div class="tool-pill vault">Vault</div>
<div class="tool-pill yaml">YAML-suppe</div>
</div>

For ti år siden var det ett script og to verktøy. Nå er det Helm, Terraform, GitOps, OPA, Vault, Argo, Istio, OTel — og forventningen om at hver utvikler skal kunne det.

<!-- Notat:

[REGI]
- nullstill perspektivet — fra org til individ
- den kognitive lasten er problemet, ikke verktøyene
- ikke ramse opp navnene mekanisk — la listen i seg selv være vitnesbyrd

[STIKKORD]
- for ti år siden: ett script, to verktøy
- nå: Helm, Terraform, GitOps, OPA, Vault, Argo, Istio, OTel
- forventning: hver utvikler skal kunne alt
- DevOps lovet samarbeid — cloud-native ga kompleksitet
- ikke verktøyenes feil — det er bare for mye for én

[BRO]
- "det er det Platform Engineering svarer på" → definisjon

-->

---

<!-- _footer: 'platformengineering.org' -->

# Platform Engineering

<div class="columns-2">

<div>

Disiplinen som bygger **golden paths** — så utviklerne kan selvbetjene det de trenger, uten å vente på ops.

Et skreddersydd lag mellom utvikler og infrastruktur. Et **produkt**, ikke et prosjekt.

</div>

<div>

<div class="diagram morph-layer full">
  <div class="box dev">DEV</div>
  <div class="arrow">&rarr;</div>
  <div class="box idp morph-idp">
    INTERNAL<br>DEVELOPER<br>PLATFORM
    <span class="morph-tool tool-k8s"></span>
    <span class="morph-tool tool-tf"></span>
    <span class="morph-tool tool-helm"></span>
    <span class="morph-tool tool-vault"></span>
    <span class="morph-tool tool-yaml"></span>
  </div>
  <div class="arrow">&rarr;</div>
  <div class="box infra">INFRA</div>
</div>

</div>

</div>

<!-- Notat:

[REGI]
- her morpher "vedlikeholder infrastruktur" inn i den røde IDP-boksen
- la diagrammet bære
- sidetekst kort, ikke les ord-for-ord

[STIKKORD]
- PE = disiplinen som bygger golden paths
- selvbetjening — uten å vente på ops
- skreddersydd lag mellom dev og infra
- produkt, ikke prosjekt
- IDP er den konkrete artefakten

[POENG]
- to nye begreper på ett slide: "golden paths" og "IDP"
- begge utdypes på neste slides — ikke forklar dem her

[BRO]
- "men hva eier teamet egentlig?" → admin/user

-->

---

# Hvert verktøy har to sider

![admin user split](svg/admin-user-split.svg)

Platform-teamet eier *å drifte* verktøyene. Produktteamene eier *å bruke* dem.

<!-- Notat:

[REGI]
- klareste forklaringen av hva platform-teamet faktisk gjør
- viktig avklaring: dette er IKKE tilbake til siloed ops
- bruk Kubernetes-eksempelet hvis publikum er teknisk

[STIKKORD]
- hvert verktøy har to sider: drifte vs bruke
- forskjellige fag — ikke samme rolle på forskjellige nivåer
- Kubernetes: egen sertifisering for cluster admin og application developer
- platform-team eier admin-siden av delte verktøy
- produktteam beholder bruker-siden
- forskjell fra gammeldags ops: vi co-designer katalogen — ingen ticketkø

[POENG]
- ops-personaen lytter ekstra her — dette er hvor jobben deres flytter seg

[BRO]
- "ok, så hva er en IDP egentlig?" → er/er ikke

-->

---

# Internal Developer Platform — en IDP

<div class="columns-2">

<div>

### Det *er*

- Anbefalte veier for det utviklere gjør oftest
- Selvbetjening — ingen tickets
- Sikkerhet og best practice innebygd fra dag én
- Et **produkt**, ikke et prosjekt

</div>

<div>

### Det *er ikke*

- En portal
- Et ticketsystem med penere UI
- Et Kubernetes-cluster noen dokumenterte
- En samling verktøy uten sammenheng

</div>

</div>

<!-- Notat:

[REGI]
- rydd opp i misforståelser før vi går videre
- venstre lander først, så høyre — kontrast
- ikke les listene — pek på 1-2 punkter per side

[STIKKORD]
- ER:
  - anbefalte veier for det utviklere gjør oftest
  - selvbetjening, ingen tickets
  - sikkerhet/best practice fra dag én
  - produkt, ikke prosjekt
- ER IKKE:
  - bare en portal (vanligste misforståelse)
  - ticketsystem med pent UI
  - et k8s-cluster noen dokumenterte
  - en samling verktøy uten sammenheng

[POENG]
- "portal ingen ba om" forhåndskoder for anti-patterns-sliden senere
- de fleste i salen tenker "vi har dette" — utfordre med "er det bygget med vilje"

[BRO]
- "men hva består en IDP egentlig av?" → fem planes

-->

---

# Anatomi av en IDP — fem planes

![idp planes](svg/idp-planes.svg)

Tre stablede planes utviklere beveger seg gjennom. To tverrgående bånd som krysser alt.

<!-- Notat:

[REGI]
- navngi planes — pillsene er kart, ikke leseliste
- pek på 1-2 pills per plane som anker, ikke alle
- pek på at Security + Observability er cross-cutting, ikke et lag på bunnen
- 60-75 sek

[STIKKORD]
- Developer Control = utviklerens inngang (workload-spec, portal, API, CLI)
- Integration & Delivery = pipeline-laget (versjonskontroll, CI, CD, orchestrator)
- Resource = der workload-en faktisk kjører (compute, db, storage, dns, nettverk, IAM)
- Security = policy + secrets + identity — tverrgående
- Observability = logger + metrikker + traces — tverrgående
- "planes" ikke "lag" — de er parallelle, ikke sekvensielle

[POENG]
- felles språk for IDP-arkitektur — fra CNCF Platform Working Group
- denne strukturen lar dere snakke om "hva mangler vi" på en strukturert måte
- pillsene blir til ports på neste slide — samme element, ny ramme

[BRO]
- "hver av disse pillsene er en port — la oss se hva som fyller dem" → ports & adapters

-->

---

# Ports & adapters — én port, mange verktøy

![ports og adapters](svg/idp-ports-adapters.svg)

Hver port er et **behov** (versjonskontroll, secrets, metrikker). Adapterne under er **valg** — utskiftbare verktøy. Når et team trenger et nytt adapter, vokser katalogen.

<!-- Notat:

[REGI]
- pek på 1-2 kolonner — ikke gå gjennom alle
- ports & adapters = hexagonal arkitektur — ramme for "abstraksjon vs implementasjon"
- viktigste poeng: porten er kontrakten, adapteret er valget
- 60-90 sek

[STIKKORD]
- port = behovet (versjonskontroll, secrets, metrikker)
- adapter = den konkrete implementasjonen (GitHub, Vault, Prometheus)
- katalogen er listen over adapters dere har hardened og støtter
- nye adapters legges til når et team trenger det — escape hatch absorbert
- bytte ett adapter bryter ikke katalogen (forutsetter porten er definert riktig)
- antimønster: "vi har valgt Backstage" som strategi — det er et adapter, ikke en strategi

[POENG]
- denne distinksjonen er hvordan dere unngår å låse dere til feil verktøy
- gjør det også enklere å bytte adapter senere uten å skifte plattform
- "vi støtter både GitHub og GitLab" er en katalog-beslutning, ikke en kompromiss

[BRO]
- "og hjertet i hvordan utviklere møter dette — golden paths" → paved road

-->

---

# Golden paths er en **paved road** — ikke et gjerde

![paved road](svg/paved-road.svg)

<div class="caption">

Veien er **anbefalt**, ikke obligatorisk. Den fungerer, dokumentasjonen finnes, vi har testet den. Det finnes alltid en utvei — og når et team trenger en, blir den utveien neste teams hovedvei.

</div>

<!-- Notat:

[REGI]
- ikke et gjerde — en vei
- escape hatches = feedback, ikke feil
- den vanligste misforståelsen er at golden path = obligatorisk

[STIKKORD]
- anbefalt, ikke obligatorisk
- veien fungerer, dokumentasjon finnes, vi har testet den
- escape hatch = utvei
- eksempel: team vil ha Circle CI istedenfor GitLab CI
  → ikke "nei", men "ok, vi setter det opp ordentlig"
  → og legger inn i platformen
- escape hatches er hvordan katalogen vokser — ikke et gap
- unntak: hvis bare ett team trenger det, eier de det selv

[POENG]
- "lite frustrerer utviklere mer enn å bli fortalt at de må gjøre det på én måte"
- paved road = invitasjon, ikke pålegg

[BRO]
- "men hva er en golden path egentlig — i én setning?" → quote

-->

---

<!-- _class: accent -->

> *En golden path er ikke en regel.*
>
> *Det er et løfte:*

## **"Gjør det slik — så har vi ryggen din."**

<!-- Notat:

[REGI]
- hjertet av filosofien
- la det lande — pause
- ikke forklar, ikke utdyp — sitatet jobber selv

[STIKKORD]
- "ikke en regel — et løfte"
- "gjør det slik — så har vi ryggen din"
- gjenta langsomt om nødvendig
- 5-10 sek stillhet er OK her

[BRO]
- klikk inn i "produkt" — løftet er bare ekte hvis platformen vedlikeholdes

-->

---

# Et **produkt**, ikke et prosjekt

![product vs project](svg/product-vs-project.svg)

<div class="caption">

Plattformen leveres ikke ferdig. Den utvikles kontinuerlig — med utviklere som kunder og adopsjon som suksessmetrikk.

</div>

<!-- Notat:

[REGI]
- mindset-skiftet — den enkeltvis viktigste setningen for CTO-publikum
- forskjell på adopsjon og hyllevare
- forhåndskoder Team Topologies-callback i timeline

[STIKKORD]
- ikke "vi bygger og leverer ferdig"
- "vi vedlikeholder et produkt for utviklerne våre"
- utviklere = kunder
- adopsjon = suksessmetrikk (ikke features levert)
- kommer fra Team Topologies, Skelton & Pais, 2019

[POENG]
- når CTO hører "produkt, ikke prosjekt" — det er der de fleste platforminitiativ feiler
- finansiering må reflektere dette: vedvarende, ikke prosjektpott

[BRO]
- "men hvor kom dette fra? la oss zoome ut" → timeline

-->

---

<!-- _class: timeline -->

# Hvordan kom vi hit?

<div class="timeline-wrap">

![timeline](svg/timeline.svg)

</div>

Platform Engineering dukket ikke opp i et vakuum. Det er svaret på et problem som har bygget seg opp i over tjue år.

<!-- Notat:

[REGI]
- sett scenen — ikke historieleksjon
- vis at PE har lineage og motiv
- tre stopp: 2009→2015, 2019, i dag

[STIKKORD]
- PE dukket ikke opp i et vakuum
- svar på problem som har bygget seg over 20+ år
- ikke buzzword — konsept med opphav

[BRO]
- klikk → 2009

-->

---

<!-- _class: timeline -->

# 2009 — DevOps

<div class="timeline-wrap">

![timeline](svg/timeline.svg)

<div class="morph-now-dot now-dot y2009"></div>

</div>

**Patrick Debois** ga navn til det alle visste: muren mellom dev og ops må ned.

Kultur. Felles ansvar. *"You build it, you run it."* Revolusjonerende.

Men så kom skyen.

<!-- Notat:

[REGI]
- åpning av lineage-fortellingen
- rolig tempo — sett scenen før smerten kommer
- ~30 sek

[STIKKORD]
- Patrick Debois, DevOpsDays Ghent
- muren mellom dev og ops må ned
- kultur, felles ansvar
- "you build it, you run it"
- revolusjonerende — for sin tid

[BRO]
- "men så kom skyen" → 2015

-->

---

<!-- _class: timeline -->

# ~2015 — "You build it, you run it" blir for mye

<div class="timeline-wrap">

![timeline](svg/timeline.svg)

<div class="morph-now-dot now-dot y2015"></div>

</div>

*Cloud ga oss alt vi trengte — og hundre nye måter å skyte oss selv i foten på.*

Kubernetes. Terraform. Helm. Service meshes. Hver utvikler forventes å være infraekspert.

Senior-devs havner i *shadow operations*. Ticket-køene vokser. Kognitiv last spiser dagen.

**DevOps var ikke feil. Det ble bare for mye for ett menneske å bære.**

<!-- Notat:

[REGI]
- smerten — alle kjenner seg igjen
- klimakset er den fete linja til slutt
- ~45 sek

[STIKKORD]
- cloud-native eksploderer
- K8s, TF, Helm, service meshes
- hver utvikler skal være infraekspert
- shadow operations på senior-nivå
- ticket-køer vokser
- kognitiv last spiser dagen
- KLIMAKS: DevOps var ikke feil — bare for mye for én

[BACKUP]
- hvis publikum trenger broen tilbake til 2009:
  "DevOps lovet utviklerne autonomi — i praksis fikk de mer ansvar og samme ventetid"

[BRO]
- "noen så at problemet var organisatorisk, ikke teknisk" → 2019

-->

---

<!-- _class: timeline -->

# 2019 — Team Topologies

<div class="timeline-wrap">

![timeline](svg/timeline.svg)

<div class="morph-now-dot now-dot y2019"></div>

</div>

<div class="columns-2">

<div>

**Matthew Skelton** og **Manuel Pais** navngir fire teamtyper — Stream-aligned, Platform, **Enabling**, og Complicated-subsystem.

Platform-teamet leverer **produktet**. **Enabling-teamet** leverer **kapabilitet** — midlertidig, til andre team kan stå på egne ben.

Plattform som produkt. Utviklere er kunder. Grunnmuren for alt vi gjør i dag.

</div>

<div>

<div class="tt-panel">

![team topologies](svg/team-topologies.svg)

</div>

</div>

</div>

<!-- Notat:

[REGI]
- nøkkelboken
- pek på TT-figuren — "for de som har lest boken"
- ett poeng: paradigmeskiftet
- 30-45 sek

[STIKKORD]
- Matthew Skelton + Manuel Pais
- fire teamtyper: Stream-aligned, Platform, Enabling, Complicated-subsystem
- Platform-team = leverer produktet (plattformen)
- Enabling-team = gir andre team kapabiliteter de mangler, midlertidig
- nøkkelidé: plattform som produkt
- utviklere = kunder, ikke kolleger
- TT-figur: stream-teams som kunder, platform-team som leverandør
- her legges grunnmuren

[POENG]
- pek kort på figuren: stream-teams blir betjent av platform-teamet
- fremhev Enabling — vi kommer tilbake til det senere (callback før overlevering)
- ikke teknisk gjennomgang av Team Topologies — bare det som ramme

[BRO]
- "konseptet fikk navn og hjem" → i dag

-->

---

<!-- _class: timeline -->
<!-- _footer: 'platformengineering.org · 280 000+ medlemmer' -->

# 2022 — Platform Engineering tar form

<div class="timeline-wrap">

![timeline](svg/timeline.svg)

<div class="morph-now-dot now-dot y2022"></div>

</div>

Gartner: top 10 strategic tech trend. platformengineering.org passerer 10 000 medlemmer i 2022 — over 280 000 nå. IDP-en blir den konkrete artefakten — **produktet** plattform-teamet leverer.

Ikke DevOps på nytt. Ikke SRE i nye klær. En egen disiplin — med utvikleren som kunde.

<!-- Notat:

[REGI]
- her tas konseptet fra teori til praksis
- 2022 er startpunktet, men momentumet fortsetter — pek på pilen til høyre
- ikke DevOps på nytt — viktig avklaring

[STIKKORD]
- 2022: Gartner top 10 strategic tech trends
- 2022: platformengineering.org passerer 10 000 medlemmer
- 2026: > 280 000 medlemmer (footer-tallet — vis veksten)
- prediksjon: 80 % av eng-organisasjoner med platform-team innen 2026
- IDP = det konkrete produktet
- egen disiplin — utvikleren som kunde
- ikke DevOps rebranded, ikke SRE i nye klær

[POENG]
- legitimering for executive-publikum: dette er ikke konsulentmote
- pilen i tidslinjen viser at 2022+ ikke er et endepunkt — vi er fortsatt i denne fasen

[BRO]
- "og dette er ikke amerikansk hype — la oss se hva som faktisk kjører i Norge i dag" → norske IDP-er (i drift)

-->

---

<!-- _class: circles -->
<!-- _footer: 'sources: {nav,equinor,sikt,enova}' -->

# Norske IDP-er — i drift

![circle](../themes/swone-assets/idp-nais.svg) ![circle](../themes/swone-assets/idp-radix.svg) ![circle](../themes/swone-assets/idp-platon.svg) ![circle](../themes/swone-assets/idp-njord.png)

### NAIS — NAV

~100 team, 1 400+ apper. Åpen kildekode siden 2017.

### Radix — Equinor

AKS-PaaS, deklarativ via `radixconfig.yaml`. MIT-lisens. Tre produksjonsclustere.

### Platon — SIKT

AWS EKS + GitLab. Fellesplattform for kunnskapssektoren. Visjon: *"Norges beste utvikleropplevelse."*

### Njord — Enova

AKS + ArgoCD + Dapr. Lansert mars 2026 som svar på digital suverenitet — bygget for leverandøruavhengighet.

<!-- Notat:

[REGI]
- proof-point — la tyngden lande
- privat (Equinor) + offentlig (NAV, SIKT, Enova)
- Njord er ferskest — digital suverenitet, ikke bare DevEx
- ikke ramse opp — pek på 1-2 detaljer per IDP

[STIKKORD]
- NAIS (NAV): ~100 team, 1 400+ apper, åpen kildekode siden 2017, NaaS til andre etater
- Radix (Equinor): AKS-PaaS, deklarativ via radixconfig.yaml, MIT, tre prod-clustere
- Platon (SIKT): AWS EKS + GitLab, fellesplattform kunnskapssektor, "Norges beste utvikleropplevelse"
- Njord (Enova): AKS + ArgoCD + Dapr, lansert 19. mars 2026, motivasjon = digital suverenitet / leverandøruavhengighet

[POENG]
- ikke amerikansk hype — norsk virkelighet
- dere er ikke først
- både privat og offentlig har bygget — på tvers av sektor

[BRO]
- "men hvorfor — hva er gevinsten?" → verdi-seksjon

-->

---

<!-- _class: invert -->

# Verdien

## For utvikler, ops, og virksomhet

<!-- Notat:

[REGI]
- section break — pause før konkret nytte
- signaliser skifte: fra hva → hvorfor det matter
- la sliden stå et øyeblikk

[STIKKORD]
- kort: "nå skal vi snakke verdi"
- pause, åndedrett

[BRO]
- klikk → triptyk

-->

---

# Samme plattform — tre vinninger

<div class="triptych">
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1100 380" font-family="Arial, Helvetica, sans-serif" style="width:100%; height:auto;">
  <defs>
    <style>
      .panel { stroke-width: 1.5; }
      .p-dev { fill: rgba(73,215,255,0.06); stroke: #49D7FF; }
      .p-ops { fill: rgba(176,167,255,0.06); stroke: #B0A7FF; }
      .p-biz { fill: rgba(247,103,94,0.06); stroke: #F7675E; }
      .heading { font-size: 22px; font-weight: 700; letter-spacing: 0.04em; fill: #FFFFFF; }
      .h-dev { fill: #49D7FF; }
      .h-ops { fill: #B0A7FF; }
      .h-biz { fill: #F7675E; }
      .item { fill: rgba(255,255,255,0.04); stroke: rgba(255,255,255,0.2); stroke-width: 1; }
      .item-text { fill: #FFFFFF; font-size: 13px; font-weight: 500; }
    </style>
  </defs>
  <g transform="translate(40, 30)">
    <rect class="panel p-dev" width="320" height="320" rx="8"/>
    <image href="icons/Green%20Resources_Dark.png" x="100" y="20" width="120" height="120" preserveAspectRatio="xMidYMid meet"/>
    <text class="heading h-dev" x="160" y="180" text-anchor="middle">UTVIKLER</text>
    <g transform="translate(20, 200)">
      <rect class="item" width="280" height="30" rx="3"/>
      <text class="item-text" x="14" y="20">⏱  Miljø på minutter, ikke dager</text>
    </g>
    <g transform="translate(20, 238)">
      <rect class="item" width="280" height="30" rx="3"/>
      <text class="item-text" x="14" y="20">🧠  Mindre kognitiv last</text>
    </g>
    <g transform="translate(20, 276)">
      <rect class="item" width="280" height="30" rx="3"/>
      <text class="item-text" x="14" y="20">🚀  Slipper å være infraekspert</text>
    </g>
  </g>
  <g transform="translate(390, 30)">
    <rect class="panel p-ops" width="320" height="320" rx="8"/>
    <image href="icons/Cloud%20Computing_Dark_V2_2.png" x="100" y="20" width="120" height="120" preserveAspectRatio="xMidYMid meet"/>
    <text class="heading h-ops" x="160" y="180" text-anchor="middle">OPS</text>
    <g transform="translate(20, 200)">
      <rect class="item" width="280" height="30" rx="3"/>
      <text class="item-text" x="14" y="20">📩  Ut av ticket-helvete</text>
    </g>
    <g transform="translate(20, 238)">
      <rect class="item" width="280" height="30" rx="3"/>
      <text class="item-text" x="14" y="20">🛡  Standardisering by design</text>
    </g>
    <g transform="translate(20, 276)">
      <rect class="item" width="280" height="30" rx="3"/>
      <text class="item-text" x="14" y="20">🎯  Tid til strategisk arbeid</text>
    </g>
  </g>
  <g transform="translate(740, 30)">
    <rect class="panel p-biz" width="320" height="320" rx="8"/>
    <image href="icons/Data_Dark.png" x="100" y="20" width="120" height="120" preserveAspectRatio="xMidYMid meet"/>
    <text class="heading h-biz" x="160" y="180" text-anchor="middle">VIRKSOMHET</text>
    <g transform="translate(20, 200)">
      <rect class="item" width="280" height="30" rx="3"/>
      <text class="item-text" x="14" y="20">⏩  Lavere lead time for change</text>
    </g>
    <g transform="translate(20, 238)">
      <rect class="item" width="280" height="30" rx="3"/>
      <text class="item-text" x="14" y="20">📉  Lavere change failure rate</text>
    </g>
    <g transform="translate(20, 276)">
      <rect class="item" width="280" height="30" rx="3"/>
      <text class="item-text" x="14" y="20">👥  Raskere onboarding av folk</text>
    </g>
  </g>
</svg>
</div>

Plattformen er **ikke en IT-kostnad.** Den er en investering i organisasjonens leveringskraft.

<!-- Notat:

[REGI]
- SVG-en bærer
- pek på hver søyle bare hvis publikum trenger det
- pointe: ikke IT-kostnad, men investering i leveringskraft
- KRITISK at alle tre personas hører seg selv her

[STIKKORD]
- utvikler: tid tilbake, mindre frustrasjon, mer flow
- ops: ikke flaskehals lenger, strategisk arbeid, DORA-metrikker opp
- business: raskere time to market, lavere risiko, governance bevart
- samme plattform — tre vinninger
- ikke en kostnad, en investering

[POENG]
- DORA: change failure rate ned, deploy frequency opp, lead time ned, MTTR ned
- nevn DORA bare hvis salen er teknisk

[BRO]
- "men hvordan måler vi det?" → ROI accent

-->

---

<!-- _class: accent -->

# ROI er ikke en innkjøpskalkyle

> *"Vi kjøpte X. Sparte vi mer enn X?"* — feil spørsmål.

## Platform-ROI er **adferdsendring i skala.**

<!-- Notat:

[REGI]
- reframe — viktigste setning for CFO/CTO-publikum
- ikke regnskapssyntese, men adferdsendring
- la "adferdsendring i skala" lande før neste klikk

[STIKKORD]
- innkjøpskalkyle = feil ramme
- "kjøpte X, sparte vi mer enn X" — feil spørsmål
- riktig spørsmål: hva endret seg fordi plattformen finnes
- adferdsendring i skala = leverage
- multiplier, ikke kostnadskutt

[BRO]
- "la oss gjøre det konkret" → tre regnestykker

-->

---

<!-- _footer: 'Tall basert på ~100 utviklere · alternativ ekstern kost · skalerer lineært' -->

# Tre regnestykker — illustrative

<div class="columns-3">

<div class="box box--success">

### Tid frigjort

100 utviklere × 2 t/uke × 50 uker × 1 500 kr/t

### **≈ 15 MNOK**

Kapasitet frigjort — ikke penger spart.

</div>

<div class="box box--warning">

### Feil unngått

20 færre alvorlige hendelser × 250 000 kr

### **≈ 5 MNOK**

Direkte, målbar risikoreduksjon.

</div>

<div class="box box--info">

### Hastighet

5 nye utviklere produktive på 1 uke i stedet for 6

### **≈ 1,5 MNOK**

Onboarding-friksjon kuttet med 6×.

</div>

</div>

<!-- Notat:

[REGI]
- vær tydelig på at tallene er illustrative — mønsteret er reelt
- ikke prøv å forsvare presisjonen
- la tallene være anker; fortellingen er poenget
- footer-disclaimer er der for de som vil regne på sitt eget tall — pek hvis noen spør
- 60-90 sek

[STIKKORD]
- TID FRIGJORT (~15 MNOK):
  - 100 utviklere × 2 t/uke × 50 uker × 1 500 kr/t
  - kapasitet — ikke spart, frigjort
  - du sparker ikke folk — du flytter timer fra friksjon til verdi
  - 1 500 kr/t = alternativ ekstern kost (konsulent-ekvivalent), ikke intern lønn
- FEIL UNNGÅTT (~5 MNOK):
  - 20 færre alvorlige hendelser × 250 000 kr
  - direkte målbar risikoreduksjon
  - "alvorlig hendelse" = nedetid + responstid + tapt produktivitet
  - executives forstår denne umiddelbart
- HASTIGHET (~1,5 MNOK):
  - 5 nye utviklere produktive på 1 uke i stedet for 6
  - 5 × 5 uker spart × 40 t × 1 500 kr/t
  - onboarding-friksjon kuttet med 6×
  - resonerer på tvers av bransjer — alle ansetter

[POENG]
- "directional confidence, ikke regnskapsprecisjon"
- dette er retning, ikke regnskap
- en eneste plattform-shift kan låse opp >2 MNOK reelt — empirisk fra felt

[BRO]
- "ok, hvordan starter vi uten å rive ned alt?" → hvordan-seksjon

-->

---

<!-- _class: invert -->

# Hvordan starter du?

## Uten å rive ned alt

<!-- Notat:

[REGI]
- section break
- vi har vist hva og hvorfor — nå hvordan
- "uten å rive ned alt" = nøkkelfrase, ofte den som beroliger CTO

[STIKKORD]
- kort, la sliden stå
- pause før klikk

[BRO]
- klikk → MVP

-->

---

# Start med en **Minimum Viable Platform**

<div class="flight-simulator">
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1100 380" font-family="Arial, Helvetica, sans-serif" style="width:100%; height:auto;">
  <defs>
    <marker id="arr" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse">
      <path d="M 0 0 L 10 5 L 0 10 z" fill="#F7675E"/>
    </marker>
    <style>
      .panel { stroke-width: 1.5; }
      .p-sim { fill: rgba(73,215,255,0.06); stroke: #49D7FF; }
      .p-real { fill: rgba(247,103,94,0.06); stroke: #F7675E; }
      .heading { font-size: 22px; font-weight: 700; letter-spacing: 0.04em; fill: #FFFFFF; }
      .h-sim { fill: #49D7FF; }
      .h-real { fill: #F7675E; }
      .stake-label { font-size: 12px; font-weight: 700; letter-spacing: 0.08em; }
      .stake-low { fill: #49D7FF; }
      .stake-high { fill: #F7675E; }
      .item { fill: rgba(255,255,255,0.04); stroke: rgba(255,255,255,0.18); stroke-width: 1; }
      .item-text { fill: #FFFFFF; font-size: 13px; font-weight: 500; }
      .arrow-text { fill: #F7675E; font-size: 13px; font-weight: 700; letter-spacing: 0.04em; }
    </style>
  </defs>
  <g transform="translate(40, 40)">
    <rect class="panel p-sim" width="430" height="300" rx="8"/>
    <image href="icons/Analysis%20Tools_Dark.png" x="150" y="30" width="130" height="130" preserveAspectRatio="xMidYMid meet"/>
    <text class="heading h-sim" x="215" y="200" text-anchor="middle">FLIGHT SIMULATOR</text>
    <text class="stake-label stake-low" x="215" y="218" text-anchor="middle">LAV INNSATS — REELL LÆRING</text>
    <g transform="translate(20, 235)">
      <rect class="item" width="190" height="24" rx="3"/>
      <text class="item-text" x="10" y="16">✔  Pilot-team, ikke alle</text>
    </g>
    <g transform="translate(220, 235)">
      <rect class="item" width="190" height="24" rx="3"/>
      <text class="item-text" x="10" y="16">✔  Bare non-prod</text>
    </g>
    <g transform="translate(20, 263)">
      <rect class="item" width="190" height="24" rx="3"/>
      <text class="item-text" x="10" y="16">✔  Reset-knapp finnes</text>
    </g>
    <g transform="translate(220, 263)">
      <rect class="item" width="190" height="24" rx="3"/>
      <text class="item-text" x="10" y="16">✔  Iterér på reell bruk</text>
    </g>
  </g>
  <g transform="translate(495, 175)">
    <line x1="0" y1="0" x2="100" y2="0" stroke="#F7675E" stroke-width="2.5" marker-end="url(#arr)"/>
    <text class="arrow-text" x="50" y="-12" text-anchor="middle">først her</text>
    <text class="arrow-text" x="50" y="22" text-anchor="middle">så her</text>
  </g>
  <g transform="translate(630, 40)">
    <rect class="panel p-real" width="430" height="300" rx="8"/>
    <image href="icons/Rocket_Light.png" x="150" y="30" width="130" height="130" preserveAspectRatio="xMidYMid meet"/>
    <text class="heading h-real" x="215" y="200" text-anchor="middle">EKTE FLYVNING</text>
    <text class="stake-label stake-high" x="215" y="218" text-anchor="middle">HØY INNSATS — KOMMER SENERE</text>
    <g transform="translate(20, 235)">
      <rect class="item" width="190" height="24" rx="3"/>
      <text class="item-text" x="10" y="16">⚠  Produksjonstrafikk</text>
    </g>
    <g transform="translate(220, 235)">
      <rect class="item" width="190" height="24" rx="3"/>
      <text class="item-text" x="10" y="16">⚠  Compliance-krav</text>
    </g>
    <g transform="translate(20, 263)">
      <rect class="item" width="190" height="24" rx="3"/>
      <text class="item-text" x="10" y="16">⚠  Ingen reset-knapp</text>
    </g>
    <g transform="translate(220, 263)">
      <rect class="item" width="190" height="24" rx="3"/>
      <text class="item-text" x="10" y="16">⚠  Ekte konsekvenser</text>
    </g>
  </g>
</svg>
</div>

Lav innsats. Lav risiko. Reell læring. **Ikke produksjon — ikke ennå.** Du finner de ødelagte kontrollene mens stakes fortsatt er lave.

<!-- Notat:

[REGI]
- flight simulator-metafor: lav risiko, reell læring
- ikke produksjon ennå
- pilot-team, ikke alle samtidig

[STIKKORD]
- MVP = bevisst startpunkt, ikke utvanning
- tre egenskaper:
  - representativ (vanlige mønstre, ikke edge cases)
  - repeterbar (kan utvides til neste team)
  - iterativ (forbedres på reell bruk)
- ett pilot-team — innovator/early adopter
- bare non-prod
- vis verdi raskt — ikke bevis at du kan bygge alt

[POENG]
- "du finner de ødelagte kontrollene mens stakes er lave" — bruk denne formuleringen

[BRO]
- "men hvor møter vi pilot-teamet?" → maturity gradient

-->

---

# Møt teamene **der de er**

<div class="figure-tight">

![maturity](svg/maturity-gradient.svg)

</div>

Plattformen formes av virkeligheten i produktteamene — ikke av idealtilstanden din. Hjelp dem flytte seg inkrementelt. Versjon 1 må kanskje støtte litt av det gamle før den fortjener å utvikle seg bort fra det.

<!-- Notat:

[REGI]
- subtilt men kritisk poeng
- vanlig feil: dra alle på en moderne plattform i ett jafs
- denne sliden er forsikring mot motstand i teamene

[STIKKORD]
- plattformen formes av virkeligheten — ikke ideelltilstand
- inkrementell flytting, ikke big bang
- v1 må kanskje støtte litt av det gamle
- senere fortjener den å utvikle seg bort fra det
- jobben er å fjerne friksjon — IKKE pålegge migrering
- press for hardt = motstand (rimeligvis)

[BRO]
- "og det leder til den vanligste feilen" → wrong way

-->

---

# Den **feile** måten å starte på

<div class="figure-tight">

![wrong vs right](svg/wrong-vs-right-start.svg)

</div>

Ikke begynn med å pålegge én CI/CD. Begynn med å fjerne den **største delte smerten**. Tjen credibility først. Standardisering kommer senere.

<!-- Notat:

[REGI]
- antipattern-vaksinasjon før vi viser Canopy
- ikke standardisering først — credibility først
- denne motvirker den klassiske "vi velger CI/CD-stack først"-feilen

[STIKKORD]
- feil åpning: "dere må alle migrere til denne ene CI/CD-en"
  → legger på arbeid uten å løse smerte
  → signaliserer regler, ikke hjelp
- riktig åpning: ta den verste delte flaskehalsen fra dem
  → eksempler: k8s-drift, secrets management, observability
- tjen retten til å standardisere
- standardisering kommer SENERE — etter du har levert verdi

[POENG]
- "tjen credibility først" = signalord for CTO som har sett initiativ feile

[BRO]
- "med det i bakhodet — la oss se på hva vi har bygget" → Canopy

-->

---

# Hva vi bygger i SoftwareOne

Vi har bygget **Canopy** — vår egen interne utviklingsplattform, på åpne standarder:

- **Kubernetes** — sky-agnostisk, ingen vendor lock-in
- **Argo CD** (Apps-of-Apps) — deklarativ, versjonert leveranse
- **Custom operatorer** — skreddersydd automasjon for plattform-workflows
- **OIDC** — føderert identitet på tvers av plattformen

PoC-en er ferdig. Nå bygger vi **produktlaget**: golden paths, dokumentasjon, feedback-løkker.

<!-- Notat:

[REGI]
- konkret — ikke salgspitch
- "vi gjør dette selv"
- mest detaljerte tekniske slide; tempo opp lett
- ~60 sek

[STIKKORD]
- Canopy = SoftwareOnes interne utviklingsplattform
- åpne standarder — ikke vendor-lock
- Kubernetes — sky-agnostisk fundament
- Argo CD med Apps-of-Apps — deklarativ leveranse, versjonert
- custom operatorer — skreddersydd plattform-automasjon (Håvard demonstrerer senere)
- OIDC — føderert identitet
- PoC ferdig — nå bygger vi produktlaget:
  - golden paths
  - dokumentasjon
  - feedback-løkker

[POENG]
- vi har laget motoren — nå pakker vi det inn for utviklere
- akkurat det vi nettopp definerte: produkt, ikke prosjekt
- bevis at vi følger vår egen lære

[BRO]
- "og vi kan hjelpe dere komme dit også" → Enabling Team as a Service

-->

---

# Enabling Team as a Service

Du trenger ikke ansette et komplett platform-team på dag én.

**SoftwareOne kan fungere som et midlertidig enabling team** — bygge MVP-en sammen med dere, etablere golden paths, og overlevere når deres eget platform-team er klart.

Callback til Team Topologies: et enabling team eksisterer for å gi andre team kapabiliteter de mangler — og oppløses, eller flyttes, når jobben er gjort.

<!-- Notat:

[REGI]
- rolig pitch — ikke salgsstil
- callback til Team Topologies-slide (2019) — pek tilbake i tid
- ~45 sek

[STIKKORD]
- dere trenger ikke ansette et helt platform-team for å komme i gang
- Enabling Team = team-typen fra Team Topologies (callback)
- oppgave: gi andre team kapabiliteter de mangler — midlertidig
- SoftwareOne kan kjøre den rollen:
  - bygge MVP sammen med dere
  - etablere golden paths
  - kunnskapsoverføring
  - overlevere til kundens eget platform-team
- ikke "vi tar over driften for alltid" — vi setter dere i stand til å eie det selv

[POENG]
- platform engineering = capability, ikke headcount
- midlertidig enabling team = lavere risiko enn å bygge et komplett team før dere vet hva dere trenger

[BRO]
- "og for å vise hvordan det kan se ut konkret, hører dere fra Håvard og Marius etter pausen" → teasers

-->

---

# Etter pausen — to konkrete eksempler

<div class="columns-2">

<div>

### Håvard — Kubernetes Operators

Hvordan reduserer vi kompleks infrastruktur til én utviklervennlig ressurs?

Live-bygg av en controller — operator-mønsteret i praksis.

</div>

<div>

### Marius — Canopy live

Fra onboarding av ny utvikler til app i prod.

Automatisk repo, CI-pipeline, og deploy via ArgoCD.

</div>

</div>

Det er ikke et ferdig produkt — vi starter en **samtale**.

<!-- Notat:

[REGI]
- kort og praktisk — ikke salgspitch
- pek på de to konkrete eksemplene — la dem teasere
- plass for screenshots fra Håvard/Marius (legges inn hvis BK rekker)
- ~30 sek

[STIKKORD]
- Håvard: operator-mønsteret — motoren under plattform-automasjon
- Marius: Canopy live — onboarding til prod, demo med ArgoCD
- begge ER kapabiliteten — bevis på at platform engineering = capability
- vi starter samtale, ikke salgssyklus

[POENG]
- handover demonstrerer "platform engineering = kapabilitet, ikke ett rolleansvar"
- ikke nevn det eksplisitt — la det være implisitt

[BRO]
- "men før vi gir over: la oss se på hva som ofte går galt" → anti-mønstre

-->

---

# **Slik feiler det** — tre mønstre

<div class="columns-3">

<div class="box box--warning">

### Bare nytt skilt

Døp om ops-teamet til platform-team. Samme tickets, samme køer.

**Adopsjon: null.**

</div>

<div class="box box--warning">

### Bygg for deg selv

Ex-ops bygger det *de* kjenner. Løser ops-problemer, ikke utviklerproblemer.

**Millioner brent.**

</div>

<div class="box box--warning">

### Portal ingen ba om

*"Developer portals er hot."* Bygges uten brukerresearch.

**Ingen brukte den.**

</div>

</div>

Tre feil. Én rotårsak: **bygget uten å snakke med utviklerne.**

<!-- Notat:

[REGI]
- 60-90 sek total
- tre kort, én per persona — ops, dev, business
- la felles rotårsak lande til slutt
- bruk warning-fargen aktivt: dette er fallgruver, ikke gode råd

[STIKKORD]
- BARE NYTT SKILT (ops-personaen):
  - døp om ops-team til platform-team
  - samme tickets, samme køer
  - "DevOps med finere navn"
  - adopsjon: null
- BYGG FOR DEG SELV (dev-personaen):
  - ex-ops bygger det de selv kjenner
  - løser ops-problemer, ikke utviklerproblemer
  - god intensjon — men feil retning
  - millioner brent
- PORTAL INGEN BA OM (business-personaen):
  - "developer portals er hot"
  - bygges uten brukerresearch
  - prestisjeprosjekt, null bruk
- ROTÅRSAK: bygget uten å snakke med utviklerne

[POENG]
- platform engineering uten samtalen er bare kostnad
- alle tre er fra "9 steps to platform engineering hell" — virkelige feilmoduser
- denne sliden er det executives husker — bruk den

[BRO]
- "så hva bør dere spørre dere selv om?" → closing accent

-->

---

<!-- _class: accent -->

> *Hvis utviklerne deres bruker tid på noe annet*
> *enn å skrive software som skaper verdi —*

## Da har dere et **plattformproblem**.

<!-- Notat:

[REGI]
- la setningen lande — pause
- ingen utdyping — sitatet jobber

[STIKKORD]
- "tid på noe annet enn verdiskapende kode = plattformproblem"
- gjenta langsomt om publikum trenger det
- pause 5+ sek

[POENG]
- omformulering av åpningshookene — løkken lukkes

[BRO]
- "her er tre spørsmål dere kan ta med dere" → tre spørsmål

-->

---

# Tre spørsmål å ta med hjem

1. Hvor lang tid tar det fra idé til kjørende tjeneste i prod?
2. Hvor mange tickets håndterer ops som ikke burde eksistert?
3. Hvor lenge før fem nye utviklere er produktive?

Svarene beskriver **plattformgapet deres.**

**Og gapet har en pris.**

<!-- Notat:

[REGI]
- konkrete diagnostiske spørsmål — de skal kunne ta dem med
- ikke svar — la spørsmålene henge
- ett spørsmål per persona (dev / ops / business)

[STIKKORD]
- 1 (dev): idé → kjørende tjeneste i prod — hvor lang tid?
- 2 (ops): tickets ops håndterer som ikke burde eksistert — hvor mange?
- 3 (business): fem nye utviklere produktive — hvor lenge?
  - skarpere variant hvis publikum er erfarent:
    "hvor lenge før første kodelinje i prod?"
- svarene = plattformgapet
- gapet har en pris

[POENG]
- la siste linje "gapet har en pris" lande hardt — det er kroken
- ikke utdyp — pause, klikk

[BRO]
- "og når dere har svarene — her er målbildet" → final

-->

---

<!-- _class: accent -->

# Målbildet

En organisasjon der utviklere skriver **software som skaper verdi** — ikke kjemper med infrastruktur under.

En plattform som er **et produkt**, ikke et prosjekt.

Raskere leveranser. Lavere risiko. Mindre teknisk gjeld.

## Det er det Platform Engineering leverer.

<!-- Notat:

[REGI]
- avslutning — lukk løkken
- "det er det Platform Engineering leverer" = mic drop
- pause før takk og spørsmål

[STIKKORD]
- utviklere skriver software som skaper verdi — ikke kjemper med infra
- plattform = produkt, ikke prosjekt
- raskere leveranser, lavere risiko, mindre teknisk gjeld
- sluttlinje: "det er det Platform Engineering leverer"

[POENG]
- løkken lukkes: åpningshookene → diagnose → svar → målbildet

[BRO]
- takk → Q&A eller direkte til pause
- ikke be om spørsmål før etter pausen hvis tid er stram

-->
