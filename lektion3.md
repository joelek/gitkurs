# Lektion 3: Distribuerad Git

Git är, som du säkert känner till, ett distribuerat versionshanteringssystem som möjliggör synkronisering av arbete mellan olika parter. I den tredje lektionen lär du dig att arbeta distribuerat med Git. Efter lektionen kommer du att kunna synkronisera ändringar du gör med ändringar andra gör på samma Git-projekt genom ett delat fjärrprojekt.

## 1. Initiera ett lokalt fjärrprojekt

* Skapa en tom katalog, förslagsvis med namnet "gitkurs-origin".
* Starta en terminal i katalogen, exempelvis genom att högerklicka och välja *Git Bash Here* som Windowsanvändare.

```
git init --bare
```

Detta initierar ett naket Git-projekt i katalogen.

Nakna projekt har till skillnad från vanliga projekt inte tre *states* utan endast ett, *repository*. Följdaktligen tillåter Git inte att man använder vissa kommandon i ett naket projekt utan tanken är istället att nakna projekt strikt ska användas för synkronisering.

```
git branch
```

Det nakna projektet saknar fördefinerade grenar och får istället grenar genom synkronisering.

## 2. Konfigurera fjärrprojekt för Alice

Git tillhandahåller en lista över fjärrprojekt (*remotes*) för varje lokalt Git-projekt. Denna lista finns endast lokalt och är grunden för att arbeta distribuerat med Git.

* Växla till en terminal med arbetskatalog "gitkurs-alice".

```
git remote
```

Listan över fjärrprojekt visas och bör vara tom om du har följt kursens steg.

Vi kommer nu att konfigurera det nakna projektet i katalogen "gitkurs-origin" som fjärrprojekt för Alice.

```
git remote add origin ../gitkurs-origin/
git remote
```

Listan över fjärrprojekt visas och innehåller nu ett fjärrprojekt med namn "origin".

```
git fetch origin
```

Detta hämtar sparade ändringar från fjärrprojektet "origin" och lagrar dessa lokalt. Då fjärrprojektet "origin" precis initierades finns det inga sparade ändringar att hämta. Det är dock oftast en bra idé att hämta sparade ändringar direkt när ett nytt fjärrprojekt läggs till.

## 3. Konfigurera synkronisering av lokal gren mot fjärrgren i fjärrprojekt

Vi har än så länge bara gett Git vetskapen om ett fjärrprojekt men har ännu inte definerat den lokala grenens fjärrgren (*upstream*), en gren i ett fjärrprojekt som den lokala grenen följer.

```
git branch --set-upstream-to origin/master
```

Fjärrprojektet "origin" är ett naket projekt som saknar grenar. Git misslyckas således med att konfigurera synkronisering för den valda lokala grenen mot grenen "master" i fjärrprojektet "origin". Vi måste istället skicka vår lokala gren till fjärrprojektet innan vi kan definera den som den lokala grenens fjärrgren.

```
git push origin master
```

Detta skickar den lokala grenen "master" till fjärrprojektet "origin".

```
git branch --set-upstream-to origin/master
```

Fjärrprojektet "origin" är fortfarande ett naket projekt med saknar inte längre grenar så Git lyckas att konfigurera den valda lokala grenens fjärrgren till fjärrgrenen "master" på fjärrprojektet "origin".

Följden av kommandon till Git är så pass vanlig att det finns ett behändigt kortkommando som gör båda sakerna på samma gång.

```
git push --set-upstream origin master
```

## 4. Klona Git-projektet för Bob

Låt säga att ytterligare en person, som vi kan kalla Bob, vill hjälpa till och bidra till arbetet på Git-projektet. Bob vill utgå från arbetet som tidigare gjorts på projektet och väljer därför att klona projektet med hjälp av projektets sökväg (*url*).

* Skapa en tom katalog, förslagsvis med namnet "gitkurs-bob".
* Starta en terminal i katalogen, exempelvis genom att högerklicka och välja *Git Bash Here* som Windowsanvändare.

```
git clone ../gitkurs-origin/ ./
```

Detta klonar Git-projektet som finns på den angivna sökvägen "../gitkurs-origin/" till den aktuella katalogen "./". Sökvägen är i det här fallet relativ och pekar på katalogen "gitkurs-origin" men är vanligtvis en HTTPS- eller SSH-sökväg.

```
git remote
```

Listan över fjärrprojekt visas och innehåller fjärrprojektet "origin" som automatiskt konfigureras när man klonar ett Git-projekt.

```
git branch
```

Listan över grenar visas och innehåller den lokala grenen master. Den lokala grenen "master" har automatiskt konfigurerats så att den följer fjärrgrenen "master" på fjärrprojektet "origin".

## 5. Låt Bob spara en ändring på fjärrprojektet

* Redigera innehållet i filen "material.txt", förslagsvis genom att lägga till en rad med texten "Hyr en ateljé.". Spara sedan filen.

```
git commit --all --message "lägger till ateljé i material"
git log --oneline
```

Detta skapar en ny sparad ändring och lägger den efter den senaste sparade ändringen på den valda lokala grenen (master). Den sparade ändringen innehåller ändringarna som gjordes i filen "material.txt".

```
git push
```

Detta skickar alla nya sparade ändringar från samtliga lokala grenar som har konfigurerats för att följa fjärrgrenar i fjärrprojekt. Om man vet precis vilken lokal gren man vill synkronisera och till vilket fjärrprojekt man vill synkronisera den kan man smidigt instruera Git att göra detta.

```
git push origin master
```

Detta skickar alla nya sparade ändringar till fjärrgrenen som konfigurerats att följa den lokala grenen "master" på fjärrprojektet "origin".

* Växla till en terminal med arbetskatalog "gitkurs-origin".

```
git log --oneline
```

Ändringarna som Bob skickade till fjärrprojektet "origin" syns direkt i den för "origin" lokala grenen "master".

## 6. Låt Alice hämta sparade ändringar från fjärrprojektet

* Växla till en terminal med arbetskatalog "gitkurs-alice".

```
git fetch origin
```

Detta hämtar sparade ändringar från fjärrprojektet "origin" och lagrar dessa lokalt.

```
git log --oneline
```

Ändringarna som Bob skickade till fjärrprojektet "origin" har hämtats men har ännu inte integrerats lokalt hos Alice. Vi behöver instruera Git att infoga fjärrgrenen "master" i den lokala grenen "master" alternativt ändra utgångspunkten för den lokala grenen "master" till fjärrgrenen "master". Vi väljer att infoga.

```
git merge origin/master
git log --oneline
```

Ändringarna som Bob skickade till fjärrprojektet "origin" har nu integrerats lokalt hos Alice. Detta skedde utan problem då infogningen var trivial (*fast-forward*).

Även denna kommandoföljd är så pass vanlig att det finns ett kortkommando som gör allting på en gång.

```
git pull origin master
```

## 7. Kort om åtkomstbegränsningar

Upplägget med att dela ett fjärrprojekt mellan flera användare lämpar sig bra för arbete i små till medelstora team där tillförlitligheten inom teamet är stor. Git i sig innehåller nämligen inga åtkomstbegränsningar utan detta hanteras istället av externa system som rättigheter på protokollnivå eller externa tjänster som GitHub.

Detta är bra då det låter Git fokusera enbart på versionshanteringsbiten men medför dessvärre att samtliga personer får fullständiga rättigheter att ändra i ett fjärrprojekt om ingen extern åtkomstbegränsing tillämpas. Detta kan vara direkt olämpligt om exempelvis någon användare av misstag råkar skriva över viktig data.

Den externa tjänsten GitHub stödjer konfiguration av regler för grenar i ett delat fjärrprojekt. Att förbjuda tvingad skrivning (*force push*) till grenen "master" för alla användare inklusive administratören är en sund utgångspunkt. Det kan även vara lämpligt att lägga till en regel som kräver att nytt innehåll på grenen "master" genomgår en granskning genom en så kallad *pull request*.
