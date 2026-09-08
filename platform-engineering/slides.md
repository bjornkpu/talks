---
marp: true
html: true
title: 'Hvorfor Platform Engineering'
description: 'Skaler utviklingsorganisasjonen — ikke kompleksiteten. Introduksjon til Platform Engineering og Internal Developer Platforms (IDPs): hvorfor golden paths og selvbetjening gir utviklerverdi, hva det betyr for utviklere, ops og virksomheten, og hvordan man starter med en Minimum Viable Platform.'
author: 'Bjørn Kristian Punsvik'
keywords: ['platform engineering', 'internal developer platform', 'IDP', 'golden paths', 'developer experience', 'DevEx', 'DevOps', 'SRE', 'platform as a product', 'team topologies', 'selvbetjening', 'developer productivity']
theme: hvorfor-platform-engineering
paginate: true
transition: fade 0.2s
---

<!-- _class: lead -->
<!-- _paginate: false -->
<!-- _header: '' -->
<!-- _footer: 'slides @ github.com/bjornkpu/talks' -->

![hero fade](../shared/images/121-GettyImages-1254770264.jpg)

# Platform Engineering

Internal Developer Platform

<div class="byline">

Bjørn Kristian Punsvik

2026-09-09

</div>

<!--
[STIKKORD]
- kort velkomst — ønsk velkommen til frokostseminaret
- dagens løp: hvorfor (meg) → pause → operators (Håvard) → Canopy live (Marius)

- Sjekke utgangspunktet:

Hvem har hørt om Platform Engineering før?

Hvis du måtte kategorisere deg:
Infrastruktur
Utvikler
Foretning
-->

---

<!-- _class: hook -->
<!-- _paginate: false -->
<!-- _header: '' -->
<!-- _footer: '' -->
<!-- _transition: 'fade 1s' -->


# Utviklerne dine er blant de dyreste ressursene du har. Hva gjør de når de <span class="morph-gap">ikke skriver kode</span>?

<!--
-->

---

<!-- _class: hook -->
<!-- _paginate: false -->
<!-- _header: '' -->
<!-- _footer: '' -->
<!-- _transition: 'fade 1s' -->


# De beste ops-folkene dine <span class="morph-gap">svarer på tickets</span>. De løser ikke arkitektur.

<!--
-->

---

<!-- _class: hook -->
<!-- _paginate: false -->
<!-- _header: '' -->
<!-- _footer: '' -->
<!-- _transition: 'fade 1s' -->


# De beste utviklerne dine bygger ikke produkt. De <span class="morph-gap">vedlikeholder infrastruktur</span>.

<!--
-->

---

<!-- _footer: '' -->
<!-- _header: '' -->
<!-- _paginate: false -->

<div class="neofetch">

<img src="../shared/images/profile.jpg" alt="Bjørn Kristian Punsvik">

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

<!--

[REGI]
rolig tempo

[STIKKORD]
- Bjørn Kristian Punsvik, konsulent hos SoftwareOne, for tiden utleid til Enova
- klassisk trent som software-utvikler fra NTNU, interreset i infra TIHLDE Drift, K8s hjemme-cluster og trives godt mot infra.
- ...og det har satt preg på alt siden:
  tech lead på skybasert energiplattform (Enoco),
  Utvikler på dataplatform og mentor integrasjonsplattform (Equinor)
  nå to team hos Enova — produkt-AI og dataplattform, moderniseringsprogrammet på siden

- "jeg ser hverdagen fra flere vinkler"

[BRO]
og det jeg ser igjen og igjen: kostnaden ved manglende plattform er ikke teknisk gjeld — det er at de beste utviklerne slutter å bygge nytt og begynner å vedlikeholde sin egen versjon av infrastrukturen. Det er det vi skal snakke om i dag.

→ klikk inn i diagnosen
-->

---

# Slik ser det ut når den ikke er bygget med vilje

![chaos](svg/chaos-10-stacks.svg)

<!--
[STIKKORD]
- hver boks = ett team som måtte bygge selv
- ikke fordi de ville — fordi alternativet var ingen plattform
- ti versjoner av samme fundament, ti måter å misforstå sikkerhet på
- security-boksen: ingen sjanse til å håndheve compliance på ti stacker
- "dette er hva 'vi har en plattform' ofte betyr i praksis"
- ti team eier appen OG runtimen — hver velger egen CI/CD, K8s-oppsett, registry, monitoring, secrets; hvert team trenger dyp kompetanse i hvert eneste lag
- selskapene som skalerte gjennom dette (Airbnb, Spotify) kom uavhengig til samme svar: legg inn et plattform-lag så utviklere self-server og ops slutter å være ticket-kø
- organisasjonen har ikke et verktøyproblem — den har et system- og koordineringsproblem

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
  <!-- 5 like lange linjer, radielt mot hjernens senter (540,372) -->
  <path class="crush-line" d="M 425 276 L 494 333"/>
  <path class="crush-line" d="M 477 236 L 515 318"/>
  <path class="crush-line" d="M 540 222 L 540 312"/>
  <path class="crush-line" d="M 603 236 L 565 318"/>
  <path class="crush-line" d="M 655 276 L 586 333"/>
  <image href="icons/Artificial%20Intelligence_Light_2.png" x="480" y="318" width="120" height="120" preserveAspectRatio="xMidYMid meet"/>
  <text class="label" x="550" y="450" text-anchor="middle" font-size="14">Hver utvikler forventes å mestre alt dette — i tillegg til å levere produkt.</text>
</svg>
<div class="tool-pill k8s">Kubernetes</div>
<div class="tool-pill tf">Terraform</div>
<div class="tool-pill helm">Helm</div>
<div class="tool-pill vault">Vault</div>
<div class="tool-pill yaml">YAML-suppe</div>
</div>

<!--
[REGI]
- nullstill perspektivet — fra org til individ

[STIKKORD]
- for ti år siden: ett script, to verktøy
- nå: Helm, Terraform, GitOps, OPA, Vault, Argo, Istio, OTel
- det operasjonelle ansvaret ble dyttet på utviklerne — og fortsatt levere produkt
- forventning: hver utvikler skal kunne alt
- for de fleste team er det ikke empowering — det er utmattende

- ikke verktøyenes feil — det er bare for mye for én person
- den kognitive lasten er problemet
- DevOps lovet samarbeid — cloud-native ga kompleksitet
- "you build it, you run it" kollapset i praksis

[BRO]
- "det er det Platform Engineering svarer på" → definisjon
-->

---

<!-- _footer: 'platformengineering.org' -->

# Platform Engineering

<div class="columns-2">

<div>

Disiplinen som bygger **golden paths** — så utviklerne får self-service på det de trenger, uten å vente på ops.

Et skreddersydd lag mellom utvikler og infra. Et **produkt**, ikke et prosjekt.

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

<!--
[STIKKORD]
- PE = disiplinen som bygger golden paths
- self-service — uten å vente på ops
- skreddersydd lag mellom dev og infra
- produkt, ikke prosjekt
- IDP er den konkrete artefakten

- plattform-teamet plukker standarder, konfigurerer skikkelig, og tilbyr dem som tjenester
- PE standardiserer de non-functional requirements: versjonskontroll, CI/CD, runtime, infra, logging/monitoring, security/compliance

[BRO]
- "Hvem eier hva?" → admin/user
-->

---

# Hvert verktøy har to sider

![admin user split](svg/admin-user-split.svg)

Platform-teamet eier *å drifte* verktøyene. Produktteamene eier *å bruke* dem.

<!--
[STIKKORD]
- hvert verktøy har to sider: drifte vs bruke
- forskjellige fag — ikke samme rolle på forskjellige nivåer
- Kubernetes: egen sertifisering for cluster admin og application developer
- to genuint forskjellige skill sets — Kubernetes har separate sertifiseringer for cluster administrator og application developer fordi de krever hver sin kunnskapsbase
- platform-team eier admin-siden av delte verktøy
- produktteam beholder bruker-siden

- i tradisjonell DevOps lever begge sidene i samme team — det er DER den kognitive lasten kommer fra
- gammel silo-ops: "ops bestemmer verktøy, gir tilgang via ticket" 
  — PE: "standardiserte tjenester, self-service, katalogen co-designes med teamene"
- forskjell fra gammeldags ops: vi co-designer katalogen av verktøy

[BRO]
- "ok, så hva er en IDP, hva er den ikke?" → er/er ikke
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

<!--
[STIKKORD]
- pek venstre: "anbefalte veier" + "produkt, ikke prosjekt"
- pek høyre: "bare en portal" / "ingen ba om" — vanligste misforståelsen

- kjennetegn på ikke-IDP: policy forkledd som workflow, Terraform-wrapper ingen ba om, portal som bare åpner en ticket et annet sted
- føles det som kontroll eller compliance theater, jobber utviklere stille rundt det — og adopsjonstallene lyver

[BRO]
- "men hva består en IDP egentlig av?" → fem planes
-->

---

# Anatomi av en IDP — fem planes

![idp planes](svg/idp-planes.svg)

Tre stablede planes utviklere beveger seg gjennom. To tverrgående bånd som krysser alt.

<!--
[STIKKORD]
- felles språk for IDP-arkitektur — fra McKinseys IDP-referansearkitektur, brukt av platformengineering.org / community
- ingen one-size-fits-all-IDP — men moderne IDP-er deler denne formen / planes
- denne strukturen lar dere snakke om "hva mangler vi" på en strukturert måte

- Developer Control = utviklerens inngang (workload-spec (kode), portal (UI), API, CLI)
  - utvikleren velger selv abstraksjonsnivå
- Integration & Delivery = pipeline-laget (versjonskontroll, CI, CD, (platform-)orchestrator)
- Resource = der workload-en faktisk kjører (compute, db, storage, dns, nettverk, IAM)
- Security = policy + secrets + identity — tverrgående
- Observability = logger + metrics + traces — tverrgående

- "planes" ikke "lag" — de er parallelle, ikke sekvensielle

[BRO]
- "hver av disse pillsene er en port — la oss se hva som fyller dem" → ports & adapters
-->

---

# Ports & adapters — én port, mange verktøy

<div class="figure-tight">

![ports og adapters](svg/idp-ports-adapters.svg)

</div>

Hver port er et **behov** (versjonskontroll, secrets, metrics). Adapterne under er **valg** — utskiftbare verktøy. Når et team trenger et nytt adapter, vokser katalogen.

<!--
[STIKKORD]
- port = behovet / kontrakten (versjonskontroll, secrets, metrics)
- adapter = den konkrete implementasjonen / valget (GitHub, Vault, Prometheus)
- katalogen er listen over adapters dere har hardened og støtter under governance
- denne distinksjonen er hvordan dere unngår å låse dere til feil verktøy
- gjør det også enklere å bytte adapter senere uten å skifte plattform
- bytte ett adapter bryter ikke katalogen
- antimønster: "vi har valgt Backstage" som strategi — det er et adapter, ikke en strategi
- "vi støtter både GitHub og GitLab" er en katalog-beslutning, ikke en kompromiss

- nye adapters legges til når et team trenger det — escape hatch absorbert

[BRO]
- "og hvordan utviklere møter katalogen — golden paths" → paved road
-->

---

# Golden paths er en **paved road** — ikke et gjerde

<div class="figure-small">

![paved road](svg/paved-road.svg)

</div>

<div class="caption">

Veien er **anbefalt**, ikke obligatorisk. Den fungerer, dokumentasjonen finnes, vi har testet den. Det finnes alltid en escape hatch — og når et team trenger en, blir den en ny golden path.

</div>

<!--
[STIKKORD]
- anbefalt, ikke obligatorisk
- paved road = invitasjon, ikke pålegg
- workflow, ikke verktøy — kan du beskrive den uten å nevne et verktøy?
- veien fungerer, dokumentasjon finnes, vi har testet den
- mål golden paths på resultat: time to first deploy, manuelle steg fjernet, frivillig adopsjon

- eksempel: team vil ha Circle CI istedenfor GitLab CI
  → ikke "nei", men "ok, vi setter det opp ordentlig"
  → og legger inn i plattformen — blir en ny golden path

- escape hatches er hvordan katalogen vokser
- escape hatch = utvei, feedback, ikke feil
- unntak: hvis bare ett team trenger det, eier de det selv
- tvungen path uten escape hatch: utviklere jobber rundt den i stillhet — adoption-tallene lyver
- utviklere sier de vil ha fleksibilitet — de vil ha fornuftige defaults
- kjernen: gjør den riktige tingen til den enkle tingen

[BRO]
- "kok ned golden path — i én setning?"
-->

---

<!-- _class: accent -->

> *En golden path er ikke en regel.*
>
> *Det er et løfte:*

## **"Gjør det slik — så er resten vårt problem."**

<!--
[REGI]
- PAUSE

[STIKKORD]
- "gjør det slik — så er resten vårt problem"
- "ikke en regel — et løfte"

[BRO]
- "løftet er bare ekte hvis platformen vedlikeholdes"
-->

---

# Et **produkt**, ikke et prosjekt

<div class="figure-small">

![product vs project](svg/product-vs-project.svg)

</div>

<div class="caption">

Plattformen leveres ikke ferdig. Den utvikles kontinuerlig — med utviklere som kunder og adopsjon som suksessmetrikk.

</div>

<!--
[STIKKORD]
- mindset-skiftet. produkt ikke prosjekt
- ikke "vi bygger og leverer ferdig"
- finansiering må reflektere dette: vedvarende, ikke prosjektpott
- "vi vedlikeholder et produkt for utviklerne våre"
- utviklere = kunder
- adopsjon = suksessmetrikk (ikke features levert, adapters)
- kommer fra ThoughtWorks Tech Radar (2017) popularisert av Team Topologies (2019)
- tre pilarer: 
  customer focus (utviklere = kunder)
  product ownership (roadmap + intern markedsføring)
  PM-disiplin (user research, metrics, iterasjon)
- plattformen konkurrerer alltid — mot cloud-tilbud, PaaS og utviklernes egne scripts; den vinner bare ved å være genuint bedre enn alternativet

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

<!--
[STIKKORD]
- PE dukket ikke opp i et vakuum
- svar på problem som har bygget seg over 20+ år

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

<!--
[STIKKORD]
- Patrick Debois, gav navn (DevOpsDays Ghent)
- muren mellom dev og ops må ned
- fokus på kultur, felles ansvar
- Werner Vogels (Amazon, 2006) "you build it, you run it"
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

<!--
[STIKKORD]
- cloud-native eksploderer
- K8s, TF, Helm, service meshes
- hver utvikler skal være infraekspert
- shadow operations på senior-nivå
- ticket-køer vokser
- kognitiv last spiser dagen
"DevOps lovet utviklerne autonomi — i praksis fikk de mer ansvar og samme ventetid"

- KLIMAKS: DevOps var ikke feil — bare for mye for én person

[BRO]
- "noen så at problemet var organisatorisk, ikke teknisk" → 2019
-->

---

<!-- _class: timeline compact -->

# 2019 — Team Topologies

<div class="timeline-wrap">

![timeline](svg/timeline.svg)

<div class="morph-now-dot now-dot y2019"></div>

</div>

<div class="columns-2">

<div>

**Matthew Skelton** og **Manuel Pais** navngir fire teamtyper — Stream-aligned, Platform, **Enabling**, og Complicated-subsystem.

Platform-teamet leverer **produktet**. **Enabling-teamet** leverer **capability** — midlertidig, til andre team kan stå på egne ben.

Plattform som produkt. Utviklere er kunder. Grunnmuren for alt vi gjør i dag.

</div>

<div>

<div class="tt-panel">

![team topologies](svg/team-topologies.svg)

</div>

</div>

</div>

<!--
[STIKKORD]
- 2019 Nøkkelbok, Matthew Skelton + Manuel Pais. Fire teamtyper:
- Stream-aligned = Et team som følger en bestemt arbeidsflyt, ofte knyttet til et område i virksomheten.
- Complicated Subsystem = Et team for deler av løsningen som krever ekstra spesialisert kunnskap.
- Enabling: Et midlertidig team som hjelper andre team når de står fast, eller trenger å lære noe nytt.
- Plattform: Et team som lager tjenester og verktøy som gjør det enklere for andre team å utvikle og levere. Plattformen skal fungere som et internt produkt som teamene har nytte av og faktisk ønsker å bruke.

- nøkkelidé: plattform som produkt
- utviklere = kunder, ikke kolleger

[BRO]
- "konseptet fikk navn og hjem" → i dag
-->

---

<!-- _class: timeline -->
<!-- _footer: 'platformengineering.org · 270 000+ medlemmer' -->

# 2022 — Platform Engineering tar form

<div class="timeline-wrap">

![timeline](svg/timeline.svg)

<div class="morph-now-dot now-dot y2022"></div>

</div>

Gartner: top 10 strategic tech trend for 2023.
platformengineering.org passerer 8 000 medlemmer i 2022 — over 270 000 nå. 
IDP-en blir den konkrete artefakten — **produktet** plattform-teamet leverer.

Ikke DevOps på nytt. Ikke SRE i nye klær. En egen disiplin — med utvikleren som kunde.

<!--
[STIKKORD]
- her tas konseptet fra teori til praksis
- okt 2022: Gartner top 10 strategic tech trends *for 2023*
- prediksjon: 80 % av eng-organisasjoner med platform-team innen 2026 (fra 45 % i 2022)
- 2022: platformengineering.org starter med 1000, passerer 8 000 medlemmer, 2026: > 270 000

- egen disiplin — utvikleren som kunde
- IDP = det konkrete produktet
- devops vs PE-aksene: 
  mål (samarbeid → self-service), 
  output (kultur → produkt),
  scope (prosessendring → engineered abstraksjonslag),
  eier ("alle" → dedikert team)
- PE beholder DevOps-ånden (samarbeid, rask feedback, delt ansvar) men anerkjenner at samarbeid alene ikke skalerer gjennom cloud-native-kompleksitet

[BRO]
- "og dette er ikke bare hype — la oss se hva som faktisk kjører i Norge i dag" → norske IDP-er (i drift)
-->

---

<!-- _class: circles -->
<!-- _footer: 'sources: {nav,equinor,sikt,enova}' -->

# Norske IDP-er — i drift

![circle](svg/idp-nais.svg) ![circle](svg/idp-radix.svg) ![circle](svg/idp-platon.svg) ![circle](svg/idp-njord.png)

### NAIS — NAV

~100 team, 1 600+ apper i produksjon. Åpen kildekode.

### Radix — Equinor

AKS-PaaS, deklarativ via `radixconfig.yaml`. MIT-lisens. To produksjonsclustere + playground.

### Platon — SIKT

AWS EKS + GitLab. Fellesplattform for kunnskapssektoren. Visjon: *"Norges beste utvikleropplevelse."*

### Njord — Enova

AKS + ArgoCD + Dapr. Lansert mars 2026 som svar på digital suverenitet — bygget for leverandøruavhengighet.

<!--
[STIKKORD]
Slogan - destilert fokus
- NAIS (NAV): åpen kildekode, NaaS til andre etater
  "én Application-spec → hele K8s-stacken"
- Radix (Equinor): AKS, deklarativ via radixconfig.yaml
  "you provide your code and a Dockerfile — Radix takes it from there"
- Platon (SIKT): AWS, fellesplattform kunnskapssektor
  "Norges beste utvikleropplevelse", "Platon gjør utvikleren god"
- Njord (Enova): AKS, motivasjon = digital suverenitet / leverandøruavhengighet
  "Du er kapteinen på ditt eget skip. Din oppgave er å navigere mot nye mål og levere verdi. Vår oppgave er å sørge for at havet er rolig, vinden er gunstig og at havnen alltid er åpen."

- dere er ikke først
- på tvers av sektor, både privat og offentlig

[BRO]
- "hva er gevinsten?" → verdi-seksjon
-->

---

<!-- _class: invert -->

# Verdien

## For utvikler, ops, og virksomhet

<img class="deco-icon deco-center" src="icons/Financial%20Target_Dark_Bar.png" alt="">

<!--
[STIKKORD]
- skifte: fra hva → hvorfor det matter
- for utvikler, ops, virksomhet.

[BRO]
- klikk → triptyk
-->

---

# Samme plattform — tre vinninger

<div class="triptych">

![triptyk](svg/triptych.svg)

<img class="icon icon-dev" src="icons/Green%20Resources_Dark.png" alt="">
<img class="icon icon-ops" src="icons/Cloud%20Computing_Dark_V2_2.png" alt="">
<img class="icon icon-biz" src="icons/Data_Dark.png" alt="">

</div>

Plattformen er **ikke en IT-kostnad.** Den er en investering i organisasjonens leveringskraft.

<!--
[STIKKORD]
- utvikler: tid tilbake, mindre frustrasjon, mer flow
- ops: ikke flaskehals lenger, strategisk arbeid, DORA-metrikker opp
  DORA: change failure rate ned, deploy frequency opp, lead time ned, MTTR ned
- foretningen: raskere time to market, lavere risiko, governance bevart

- samme plattform — tre vinninger
- pointe: ikke IT-kostnad, men investering i leveringskraft

[BRO]
- "men hvordan måler vi det?" →
-->

---

<!-- _class: accent -->

# ROI er ikke en innkjøpskalkyle

> *"Vi kjøpte X. Sparte vi mer enn X?"* — feil spørsmål.

## Platform-ROI er **adferdsendring i skala.**

<!--
[STIKKORD]
- innkjøpskalkyle = feil ramme
- "kjøpte X, sparte vi mer enn X" — feil spørsmål
- riktig spørsmål: hva endret seg fordi plattformen finnes
- adferdsendring i skala, leverage
- ikke kostnadskutt - mindset: du bygger en multiplier (AI) — multipliers vises i throughput og tillit, ikke i regneark

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

<!--
[STIKKORD]
- modellen er platformengineering.org sin ROI-tilnærming
- TID FRIGJORT (~15 MNOK):
  - 100 utviklere × 2 t/uke × 50 uker × 1 500 kr/t
  - kapasitet — ikke spart, frigjort
  - du sparker ikke folk — du flytter timer fra friksjon til verdi
  - 1 500 kr/t = ekstern kost
- FEIL UNNGÅTT (~5 MNOK):
  - 20 færre alvorlige hendelser × 250 000 kr
  - "alvorlig hendelse" = nedetid + responstid + tapt produktivitet
- HASTIGHET (~1,5 MNOK):
  - 5 nye utviklere produktive på 1 uke i stedet for 6
  - 5 × 5 uker spart × 40 t × 1 500 kr/t
  - onboarding-friksjon kuttet med 6×

[BRO]
- "ok, overbevist? hvordan starter vi uten å rive ned alt?" → hvordan-seksjon
-->

---

<!-- _class: invert -->

# Hvordan starter du?

## Uten å rive ned alt

<img class="deco-icon deco-center" src="icons/Planning_Dark.png" alt="">

<!--

[REGI]
PAUSE

[BRO]
- klikk → MVP

-->

---

# Start med en **Minimum Viable Platform**

<div class="flight-simulator">

![flight simulator](svg/flight-simulator.svg)

<img class="icon icon-sim" src="icons/Analysis%20Tools_Dark.png" alt="">
<img class="icon icon-real" src="icons/Rocket_Light.png" alt="">

</div>

Lav innsats. Lav risiko. Reell læring. **Ikke produksjon — ikke ennå.** Du finner de ødelagte kontrollene mens stakes fortsatt er lave.

<!--
[STIKKORD]
- MVP = bevisst startpunkt, ikke utvanning
- "du finner feilene mens konsekvensene er lave"
- tre egenskaper:
  - representativ (vanlige mønstre, ikke edge cases)
  - repeterbar (kan utvides til neste team)
  - iterativ (forbedres på reell bruk)
- ett pilot-team — early adopter
- PE teamet bør være senior infra med sterke meninger. pga valg.
- bare non-prod
- vis verdi raskt — ikke bevis at du kan bygge alt
- vanligste MVP-feil: rushe til kompleksitet, antall verktøy ≠ outcomes, glemme brukerne

[BRO]
- "men hvor møter vi pilot-teamet?" → maturity gradient
-->

---

# Møt teamene **der de er**

<div class="figure-tight">

![maturity](svg/maturity-gradient.svg)

</div>

Plattformen formes av virkeligheten i produktteamene — ikke av idealtilstanden din. Hjelp dem flytte seg inkrementelt. Versjon 1 må kanskje støtte litt av det gamle før den fortjener å utvikle seg bort fra det.

<!--
[STIKKORD]
- plattformen formes av virkeligheten — ikke ideelltilstand
- inkrementell flytting, ikke big bang
- v1 må kanskje støtte litt av det gamle
- senere fortjener den å utvikle seg bort fra det
- jobben er å fjerne friksjon — IKKE pålegge migrering
- press for hardt = motstand

[BRO]
- "og det leder til den vanligste feilen" → wrong way
-->

---

# **Feil** måte å starte på

<div class="columns-2">

<div class="box box--warning">

### ✗ Feil åpningstrekk

*«Velg én CI/CD — og migrer alle.»*

Løser ingen smerte teamene faktisk føler. Legger på arbeid.

**Møtes med motstand.**

</div>

<div class="box box--success">

### ✓ Riktig åpningstrekk

*«Vi tar den verste delte smerten.»*

K8s-drift, secrets, observability. Fjerner arbeid fra dag én.

**Tjener credibility.**

</div>

</div>

Standardisering kommer senere — først må du tjene retten til den.

<!--
[STIKKORD]
- feil åpning: regler, ikke hjelp
- riktig åpning: ta den verste flaskehalsen FRA dem
- tjen retten til å standardisere — etter du har levert verdi

- kandidater for "verste delte smerte": verktøy mange team allerede bruker dårlig — K8s cluster ops, secrets management, observability-oppsett
- standardiser før du har tjent kreditten, og du blir ignorert — teamene har ikke overlødig-kapasitet til å migrere før du har frigjort den

[BRO]
- "la oss se på hva vi har bygget" → Canopy
-->

---

# Hva vi bygger i SoftwareOne

<img class="deco-icon deco-mid" src="icons/Build%20Cloud_Dark.png" alt="">

Vi har bygget **Canopy** — vår egen interne utviklingsplattform, på åpne standarder:

- **Kubernetes** — sky-agnostisk, ingen vendor lock-in
- **Argo CD** (Apps-of-Apps) — deklarativ, versjonert leveranse
- **Custom operatorer** — skreddersydd automasjon for plattform-workflows
- **OIDC** — føderert identitet på tvers av plattformen

PoC-en er ferdig. Nå bygger vi **produktlaget**: golden paths, dokumentasjon, feedback loops.

<!--

[STIKKORD]
- Canopy = SoftwareOnes interne utviklingsplattform
- åpne standarder — ikke vendor-lock
- Kubernetes — sky-agnostisk fundament
- Argo CD med Apps-of-Apps — deklarativ delivery
- custom operatorer — skreddersydd plattform-automasjon (Håvard demonstrerer senere)
- OIDC — identitet
- PoC ferdig:
  - golden paths
  - dokumentasjon
  - feedback loops

Ikke poenget. Er et produkt, men ikke noe vi vil selge.

[BRO]
- "vi kan hjelpe dere komme dit også"

-->

---

# Enabling Team as a Service

<img class="deco-icon deco-low" src="icons/Effective%20Recruitment_Light.png" alt="">

Du trenger ikke ansette et komplett platform-team på dag én.

**SoftwareOne kan fungere som et midlertidig enabling team** — bygge MVP-en sammen med dere, etablere golden paths, og overlevere når deres eget platform-team er klart.

Callback til Team Topologies: et enabling team eksisterer for å gi andre team capabilities de mangler — og oppløses, eller flyttes, når jobben er gjort.

<!--
[STIKKORD]
- dere trenger ikke ansette et helt platform-team for å komme i gang
- Enabling Team
- oppgave: gi andre team capabilities de mangler — midlertidig
- SoftwareOne kan kjøre den rollen:
  - bygge MVP sammen med dere
  - etablere golden paths
  - kunnskapsoverføring
  - overlevere til platformen til dere
- ikke "vi tar over driften for alltid" — vi setter dere i stand til å eie det selv
- midlertidig enabling team = lavere risiko enn å bygge et komplett team før dere vet hva dere trenger

[BRO]
- "og for å vise hvordan det kan se ut konkret, hører dere fra Håvard og Marius etter pausen" →
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

<!--
[STIKKORD]
- Håvard: operator-mønsteret — motoren under plattform-automasjon
- Marius: Canopy live — onboarding til prod, demo med ArgoCD

- Selger ikke Canopy. Brukes til å starter samtale

[BRO]
- "men før vi gir over: la oss se på hva som ofte går galt" → anti-mønstre
-->

---

# **Slik feiler det** — tre mønstre

<div class="columns-3">

<div class="box box--warning">

### Bare nytt skilt

Døp om ops-teamet til platform-team. Samme tickets, samme køer.

**Samme kø, nytt navn.**

</div>

<div class="box box--warning">

### Bygg for deg selv

Ex-ops bygger det *de* kjenner. Løser ops-problemer, ikke utviklerproblemer.

**Et år arbeid, feil problem.**

</div>

<div class="box box--warning">

### Portal ingen ba om

*"Developer portals er hot."* Bygges uten brukerresearch.

**Demo imponerte. Ingen logget inn igjen.**

</div>

</div>

Tre feil. Én rotårsak: **bygget uten å snakke med utviklerne.**

<!--
[STIKKORD]
- Hjelper ikke å omdøpe OPS teamet til PE.
- OPS Løser ops problemer, ikke utviklerproblemer. god intensjon — feil retning
- Starte med en portal. imponerende demo, ingen brukere.

- to grunnårsaker bak nesten alle feilmodusene: 
  hoppe over platform-as-a-product-mindsetet, og hoppe over kommunikasjonsarbeidet

[BRO]
- "så, tilbake til åpningen" → closing accent
-->

---

<!-- _class: accent -->

> *Hvis utviklerne dine bruker tid på noe annet*
> *enn å skrive software som skaper verdi*

## Da har du et **plattformproblem**.

<!--
[STIKKORD]

Hvis utviklerne dine bruker tid på noe annet enn å skrive software som skaper verdi

Da har du et plattformproblem

[BRO]
- "her er tre spørsmål for å finne problemet" → tre spørsmål

-->

---

# Tre spørsmål å ta med hjem

<img class="deco-icon deco-mid" src="icons/Clock_Dark.png" alt="">

1. Hvor lang tid tar det fra idé til kjørende tjeneste i prod?
2. Hvor mange tickets håndterer ops som ikke burde eksistert?
3. Hvor lenge før fem nye utviklere er produktive?

Svarene beskriver **plattformgapet deres.**

<!--
1. Hvor lang tid tar det fra idé til kjørende tjeneste i prod?
2. Hvor mange tickets håndterer ops som ikke burde eksistert?
3. Hvor lenge før fem nye utviklere er produktive?

Svarene beskriver plattformgapet.
og gapet har en pris

[BRO]
- "og når dere har svarene — her er målbildet man skal strekke seg etter" → final
-->

---

<!-- _class: accent has-deco -->

# Målbildet

<img class="deco-icon deco-center" src="icons/Financial%20Target_Dark_Target.png" alt="">

En organisasjon der utviklere skriver **software som skaper verdi** — ikke kjemper med infrastruktur under.

En plattform som er **et produkt**, ikke et prosjekt.

Raskere leveranser. Lavere risiko. Mindre teknisk gjeld.

## Det er det Platform Engineering leverer.

<!--
En organisasjon der utviklere skriver software som skaper verdi — ikke kjemper med infrastruktur under.

En plattform som er et produkt, ikke et prosjekt.

Raskere leveranser. Lavere risiko. Mindre teknisk gjeld.

Det er det Platform Engineering leverer.

[BRO]
- takk →
-->

---

<!-- _class: lead -->
<!-- _paginate: false -->
<!-- _header: '' -->
<!-- _footer: 'slides @ github.com/bjornkpu/talks' -->
![hero fade](../shared/images/121-GettyImages-1254770264.jpg)

# Takk

<div class="byline">

Bjørn Kristian Punsvik
</div>

<!--
[STIKKORD]
- Håvard og Marius fortsetter etter pausen
-->

