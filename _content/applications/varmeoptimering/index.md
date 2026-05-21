---
title: "Brugervejledning – Varmeoptimering"
---

# Brugervejledning – Appen “Varmeoptimering”

## Introduktion

Appen **Varmeoptimering** anvendes til overvågning og optimering af varmeforbrug, temperaturer, alarmer og økonomi i et varmeanlæg.

Formålet er at give et hurtigt overblik over anlæggets status samt mulighed for at justere indstillinger, så energiforbruget reduceres uden at gå på kompromis med komfort eller driftssikkerhed.

Appen kan anvendes på mobil, tablet og computer.

---

## Hovedfunktioner

### Dashboard

Forsiden viser de vigtigste driftsdata:

- Aktuel fremløbstemperatur
- Aktuel returtemperatur
- Delta T (forskel mellem fremløb og retur)
- Udetemperatur
- Driftstilstand
- Drift score
- Alarmer og advarsler
- Temperaturhistorik

Dashboardet opdateres automatisk.

![Dashboard – Driftstatus, temperaturer og aktive alarmer](dashboard-driftstatus-temperatur-alarmer.png)
*Figur 1: Overblik over driftstatus, drift score, temperaturhistorik og aktive alarmer.*

---

## Menuoversigt

### 1) Status

Viser den aktuelle driftstilstand i realtid.

#### Felter og hvad de betyder

- **Overvågning (ON/OFF):** Aktiverer/deaktiverer aktiv overvågning i appens logik.
- **Anlægstype:** Vælg fx varmepumpe, kedel eller hybrid. Bruges til korrekt beregningslogik.
- **Varmekilde:** Viser registreret varmekilde-status.
- **Aktuel status:** Samlet driftsstatus (OK, advarsel, alarm).
- **Alarmårsag:** Kort tekst om seneste/aktuelle fejlårsag.
- **Anbefaling:** Systemets forslag til handling.

#### Knapper

- **Kvitter:** Kvitterer aktiv alarm, hvis alarmtype tillader det.
- **Pause (x tid):** Undertrykker alarmnotifikationer i valgt periode.
- **Reset:** Nulstiller alarmtilstand eller intern styring (afhænger af integration).

#### Farveindikering

- Grøn = normal drift
- Gul = advarsel
- Rød = alarm/fejl

---

### 2) Temperaturer

Viser temperaturmålinger samt trends.

#### Felter og input

- **Fremløb sensor entity:** Entity-id for fremløbstemperatur.
- **Returløb sensor entity:** Entity-id for returtemperatur.
- **Ude sensor entity:** Entity-id for udetemperatur.
- **Pumpeeffekt sensor entity:** Entity-id for effektmåling (W).

> Inputformat: Brug gyldige entity-id’er fra dit automationssystem (fx `sensor.kedel_fremlob`).

#### Temperaturgrænser

- **Min fremløb (°C):** Laveste ønskede fremløbstemperatur.
- **Maks fremløb (°C):** Øvre grænse for fremløb.
- **Maks returløb (°C):** Maks tilladt returtemperatur før advarsel/alarm.
- **Min delta T (°C):** Mindste temperaturdifferens før lav-delta-T alarm.
- **Maks delta T (°C):** Øvre differensgrænse.
- **Hysterese (°C):** Buffer som reducerer pendling mellem tilstande.
- **Frostgrænse (°C):** Udetemperaturgrænse for frostsikring.

#### Historikvisning

Brugeren kan:

- Se aktuelle værdier
- Se min/maks i perioden
- Sammenligne temperaturkurver over tid

![Opsætning – Sensorregistrering, temperaturgrænser og notifikationer](opsaetning-sensorer-graenser-notifikationer.png)
*Figur 2: Konfiguration af sensorer, temperaturgrænser, driftvalg og notifikationer.*

---

### 3) Varmeindstillinger

Her justeres den daglige drift.

#### Driftvalg og felter

- **Varmeoptimering aktiv (toggle):** Slår optimeringsalgoritme til/fra.
- **Frostsikring aktiv (toggle):** Beskytter anlæg ved lav udetemperatur.
- **Anlægstype:** Skal matche den fysiske installation.
- **Standard statistikperiode:** Fx 24 timer / 7 dage.

#### Sådan ændres en værdi

1. Tryk på feltet
2. Indtast ny værdi eller vælg fra dropdown
3. Gem ændringen

Ændringen aktiveres normalt med det samme.

---

### 4) Energiforbrug

Viser energi- og driftsforbrug.

#### Typiske målinger

- Forbrug denne time
- Forbrug 24 timer
- Forbrug 7 dage
- Pumpeeffekt over tid
- Estimeret varmeproduktion
- SCOP (effektivitetstal)

#### Hvad ser du i graferne?

- **Spidser i effektkurve:** Kortvarig høj last/start-stop drift.
- **Jævne kurver:** Stabil drift og bedre regulering.
- **Lav SCOP:** Kan indikere høj fremløbstemperatur, dårlig afkøling eller forkert indregulering.

---

### 5) Alarmer

Viser aktive og historiske alarmer.

#### Eksempler på alarmer

- Høj temperatur
- Lav temperatur
- Kommunikationsfejl
- Sensorfejl
- Pumpestop
- Delta T for lav/høj
- Frost risiko

#### Alarmhåndtering

1. Åbn alarmen
2. Læs fejlbeskrivelse
3. Følg anbefalet handling
4. Kvitter alarm, hvis muligt

---

### 6) Økonomi

Sektionen **Økonomi** giver overblik over pris, forbrug, lager og estimerede omkostninger.

#### A) Økonomi overblik

- **Aktuel effekt:** Nuværende effektforbrug (W/kW).
- **Drift aktiv:** Viser om anlægget kører nu.
- **Aktuel elpris:** Pris pr. kWh brugt i beregning.
- **Forbrug denne time / 24 timer / 7 dage:** Energiforbrug i perioder.
- **Omkostning denne time / 24 timer / 7 dage:** Beregnede energiomkostninger.

**Hvad ser man?**
Du får et hurtigt “her-og-nu” billede af, hvad anlægget koster at drive på kort og mellemlang horisont.

#### B) Elpris og Nord Pool

- **Pristype:** Vælg prisgrundlag (fx Nord Pool eller fast pris).
- **Nord Pool pris sensor:** Entity-id med spotpris.
- **Fast elpris:** Manuel pris ved fast aftale.
- **Tillæg pr. kWh:** Net-/transport-/abonnementstillæg.
- **Moms faktor:** Typisk 1,25.
- **Beregnet elpris:** Den samlede anvendte pris i appen.

**Inputformat:**
- Prisfelter angives som decimaltal (fx `2,50` kr/kWh)
- Entity-felter angives som gyldigt sensor-id.

#### C) Måling

- **Effekt sensor:** Sensor for aktuelt effektforbrug.
- **Driftgrænse (W):** Minimumseffekt for at tælle som “drift”.
- **Driftstid 1 time / 24 timer / 7 dage:** Akkumuleret driftstid.
- **Starter 24 timer:** Antal starter (indikator for start/stop-frekvens).

**Hvad ser man?**
Om anlægget kører stabilt eller ofte starter/stopper. Mange starter kan øge slid.

#### D) Brændsel og priser

- **Brændselstype:** Fx el, olie, piller, halm.
- **Brændselsprisfelter:** Pris pr. enhed (kr/l, kr/kg, kr/enhed).
- **Brændværdi:** Energiindhold pr. enhed (kWh/enhed).
- **Brændsel ved drift:** Forbrugshastighed under drift (enhed/time).
- **Virkningsgrad:** Anlæggets effektivitet (0–1 eller % afhængig af opsætning).
- **Aktiv brændselspris:** Beregnet effektiv pris pr. enhed.

**Hvad ser man?**
En sammenlignelig omkostning på tværs af brændselstyper.

#### E) Lager og genopfyldning

- **Lagerkapacitet:** Max beholdning.
- **Aktuel beholdning:** Nuværende lager.
- **Normal påfyldning:** Typisk mængde pr. påfyldning.
- **Lager procent:** Fyldningsgrad i %.
- **Resterende timer/dage:** Estimat baseret på aktuelt forbrug.
- **Cirka næste påfyldning:** Datoestimat.
- **Beholdning efter påfyldning:** Forventet niveau efter næste refill.

**Hvad ser man?**
Hvornår du forventeligt løber tør, og hvornår påfyldning bør planlægges.

#### F) Brændselsforbrug

- **Brændsel 1 time / 24 timer / 7 dage:** Forbrug i valgte perioder.
- **Brændselsomkostning 1 time / 24 timer / 7 dage:** Kroneforbrug pr. periode.

#### G) SCOP og varmeproduktion

- **Estimeret varmeproduktion 24t:** Produceret varmeenergi i perioden.
- **SCOP 24t:** Sæsonkorrigeret effektivitet i perioden.

**Tolkning:**
- Højere SCOP = mere varme pr. kWh el/brændsel.
- Faldende SCOP over tid kan indikere behov for service eller justering.

![Økonomi – Elpris, forbrug, lager, brændsel og SCOP](okonomi-elpris-forbrug-lager-scop.png)
*Figur 3: Økonomioversigt med elpris, forbrug, omkostninger, lager og nøgletal for produktion.*

![Statistik – Temperaturer, delta T, drift score og alarmhistorik](statistik-temperatur-deltaT-driftscore-alarmhistorik.png)
*Figur 4: Statistikvisning med trends for temperatur, delta T, pumpeeffekt, drift score og alarmhistorik.*

---

## Notifikationer

Appen kan sende beskeder ved:

- Fejl på anlæg
- Temperaturafvigelser
- Højt energiforbrug
- Manglende kommunikation

Notifikationstyper:

- Push-besked
- E-mail
- SMS (hvis aktiveret)

### Notifikationsfelter

- **Notifikation aktiv:** Master-toggle for alarmer.
- **Notifikation service:** Service-navn der kaldes ved alarm.
- **Gentag alarm hvert (min):** Hvor ofte alarm gentages.
- **SMS aktiv:** Aktiverer SMS-kanal.
- **SMS service:** API/service til SMS-afsendelse.
- **GatewayAPI afsender:** Visningsnavn hos modtager.
- **GatewayAPI prioritet:** Fx lav/normal/høj.
- **SMS modtagere:** Telefonnummerliste.
- **Antal SMS modtagere:** Automatisk optælling.

**Input for SMS-modtagere:**
Brug internationalt format, fx `+4512345678`. Flere numre kan adskilles med komma, semikolon eller linjeskift.

---

## Brugerroller

### Administrator

Har adgang til:

- Alle indstillinger
- Brugeradministration
- Avanceret opsætning
- Systemkonfiguration

### Driftspersonale

Har adgang til:

- Overvågning
- Alarmhåndtering
- Daglig drift
- Basisindstillinger

### Gæst/Viewer

Kan kun:

- Se status
- Se temperaturer
- Se grafer
- Se økonomi (read-only)

Ingen ændringer kan foretages.

---

## Praktisk brug

### Daglig kontrol

Det anbefales dagligt at kontrollere:

- At anlægget er i normal drift
- At temperaturer er stabile
- At der ikke er aktive alarmer
- At energiforbruget virker normalt
- At økonomital ikke afviger unormalt

---

## Gode råd til varmeoptimering

- Undgå unødigt høj fremløbstemperatur
- Brug nat-/dagsænkning
- Hold stabile temperaturer
- Reagér hurtigt på alarmer
- Kontrollér returtemperaturen regelmæssigt
- Følg udvikling i SCOP og starter pr. døgn

---

## Fejlfinding

### Ingen data vises

Kontrollér:

- Internetforbindelse
- Strøm til anlæg
- Gateway/controller
- Sensorforbindelser
- Korrekte entity-id’er i opsætning

### Forkerte temperaturer

Kontrollér:

- Sensorplacering
- Sensorfejl
- Kabelforbindelser
- Kalibrering
- Enheder (°C, kWh, W)

### Appen kan ikke forbindes

Prøv:

1. Genstart appen
2. Kontrollér netværk
3. Genstart controller/gateway
4. Kontakt administrator

---

## Sikkerhed

- Del ikke loginoplysninger
- Brug stærke adgangskoder
- Log ud på fælles enheder
- Kun autoriserede brugere må ændre indstillinger

---

## Support

Ved fejl eller spørgsmål kontaktes:

- Systemadministrator
- Installatør
- Servicepartner

Hav gerne følgende klar:

- Fejlbeskrivelse
- Tidspunkt for fejl
- Eventuelle alarmkoder
- Screenshots fra appen
- Hvilke felter/værdier der blev ændret før fejlen
