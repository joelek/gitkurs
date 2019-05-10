# Gitkurs

Välkommen till den här kursen i Git-hantering via terminalen! Vi ska tillsammans gå igenom tre lektioner som förhoppningsvis tar dig från glad nybörjare till kvalificerat proffs.

## 1. Förberedelser

* Installera [Git](https://git-scm.com/).

## 2. Hjälp

Det kan vara bra att veta att varje Git-kommando har ett hjälpavsnitt som enkelt kan visas i terminalen.

```
git <kommando> -h
```

## 3. Lektioner

Innan vi börjar med lektionerna kan det vara bra att gå igenom vad versionshantering faktiskt är och vilka fördelar som finns med att använda ett system för [versionshantering](versionshantering.md).

* [Lektion 1: Ändringars tre tillstånd](lektion1.md)
* [Lektion 2: Lokala grenar](lektion2.md)
* [Lektion 3: Distribuerad Git](lektion3.md)

## 4. Rekommenderad arbetsmetod

* Projekt skapas på GitHub.
* Projekt konfigureras för att endast tillåta *squash merging*.
* Arbete sker på arbetsgrenar med namngivningsschema "wip-*".
* Infogning av master i arbetsgrenar sker kontinuerligt under arbetets gång.
* Granskning av arbetsgrenar sker genom *pull requests* på GitHub.
* Kompletting vid granskning sker genom att ytterligare ändringar skickas upp på respektive arbetsgren.

Vid licensering av GitHub bör följande även konfigureras för varje projekt. Dessa funktioner är inte tillgängliga för icke-betalande användare.

* En regel sätts för grenen "master" som kräver granskning av samtliga ändringar.
* Ytterligare en regel sätts för övriga grenar "*" som förhindrar tvingande skrivning (*force push*).
