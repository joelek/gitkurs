# Lektion 2: Lokala grenar

I kursens andra lektion lär vi oss att arbeta med grenar i Git. Efter lektionen kommer du att kunna använda Git för lokal, icke-linjär versionshantering.

## 1. Skapa en ny gren

```
git branch bakgrund
git branch
```

* Detta skapar en ny gren med utgångspunkt i den aktiva versionen. Den aktiva versionen är i det här fallet den senaste sparade ändringen på den förvalda grenen (master).

## 2. Ändra vald gren

```
git checkout bakgrund
git branch
```

* Detta sätter den valda grenen till bakgrund.

## 3. Ändringar sparas på den valda grenen

* Skapa en fil med namnet "bakgrund.txt".

```
git add bakgrund.txt
git commit --message "skapar bakgrund.txt"
```

* Detta skapar en ny sparad ändring och lägger den efter den senaste sparade ändringen på den valda grenen (bakgrund). Den sparade ändringen innehåller den tomma filen "bakgrund.txt".
* Redigera innehållet i filen "bakgrund.txt", förslagsvis genom att lägga till en rad med texten "Rita en bergskedja i den övre delen av tavlan.". Spara sedan filen.

```
git commit --all --message "lägger till bergskedja till bakgrund"
git log --oneline
```

* Detta skapar en ny sparad ändring och lägger den efter den senaste sparade ändringen på den valda grenen (bakgrund). Den sparade ändringen innehåller ändringarna som gjordes i filen "bakgrund.txt".
* Redigera innehållet i filen "bakgrund.txt" en gång till, förslagsvis genom att lägga till en rad med texten "Rita några kullar i den nedre delen av tavlan.". Spara sedan filen.

```
git commit --all --message "lägger till kullar till bakgrund"
git log --oneline
```

* Detta skapar en ny sparad ändring och lägger den efter den senaste sparade ändringen på den valda grenen (bakgrund). Den sparade ändringen innehåller ändringarna som gjordes i filen "bakgrund.txt".

## 4. Arbete kan fortskrida från valfri sparad ändring

```
git checkout head~1
git log --oneline
```

* Detta sätter den aktiva versionen till den näst senaste sparade ändringen på den valda grenen (bakgrund). Efter kommandot är Git i ett frikopplat läge och har inte längre en vald gren.

## 5. Nya grenar skapas med utgångspunkt i den aktiva versionen

```
git branch objekt
git branch
```

* Detta skapar en ny gren med utgångspunkt i den aktiva versionen. Den aktiva versionen är i det här fallet den senaste sparade ändringen i ett frikopplat läge utan vald gren.

```
git checkout objekt
git branch
```

* Detta sätter den valda grenen till objekt.

## 6. Grenar tillåter parallellt arbete

* Skapa en fil med namnet "objekt.txt".

```
git add objekt.txt
git commit --message "skapar objekt.txt"
```

* Detta skapar en ny sparad ändring och lägger den efter den senaste sparade ändringen på den valda grenen (objekt). Den sparade ändringen innehåller den tomma filen "objekt.txt".
* Redigera innehållet i filen "objekt.txt", förslagsvis genom att lägga till en rad med texten "Rita en sol i det övre högra hörnet.". Spara sedan filen.

```
git commit --all --message "lägger till en sol till objekt"
git log --oneline
```

* Detta skapar en ny sparad ändring och lägger den efter den senaste sparade ändringen på den valda grenen (objekt). Den sparade ändringen innehåller ändringarna som gjordes i filen "objekt.txt".

## 7. Grenar kan infogas

```
git checkout bakgrund
git branch
```

* Detta sätter den valda grenen till bakgrund.

```
git merge objekt --message "grenen objekt infogas"
git log --oneline
```

* Detta infogar samtliga sparade ändringar på grenen "objekt" till den valda grenen (bakgrund).

> Fram tills nu har Git varit relativt tillmötesgående med de kommandon som vi har matat in. Infogning av grenar är dock en av ett fåtal operationer där Git faktiskt kan få problem med att fullfölja instruktionerna utan handpåläggning. Lyckligtvis har denna kurs än så länge utformats så att kommandot ska gå att köra utan problem.

## 8. En grens utgångspunkt kan ändras

```
git checkout objekt
git branch
```

* Detta sätter den valda grenen till objekt.

```
git rebase bakgrund~1
git log --oneline
```

* Detta sätter utgångspunkten för den valda grenen (objekt) till den näst senaste sparade ändringen på grenen "bakgrund". Den näst senaste sparade ändringen väljs då grenen "bakgrund" efter infogning innehåller en så kallad *merge commit*. 

> En *merge commit* skapas när infogning sker mellan två grenar där infogningen är icke-trivial, eller på Git-språk *non-fast-forward*.

> Ändring av utgångspunkter för grenar är en annan av de operationer där Git kan få problem med att fullfölja instruktionerna utan handpåläggning. Kommandot ska dock gå att köra utan problem tack vare hur kursen har utformats.

## 9. Konflikter kan uppstå när ändringar görs parallellt

```
git checkout master
git branch
```

* Detta sätter den valda grenen till master.

```
git branch extramaterial
git branch
```

* Detta skapar en ny gren med utgångspunkt i den aktiva versionen. Den aktiva versionen är i det här fallet den senaste sparade ändringen på den valda grenen (master).
* Redigera innehållet i "material.txt", förslagsvis genom att lägga till en rad med texten "Införskaffa ett stafli.". Spara sedan filen.

```
git commit --all --message "lägger till ett stafli i material"
git log --oneline
```

* Detta skapar en ny sparad ändring och lägger den efter den senaste sparade ändringen på den valda grenen (master). Den sparade ändringen innehåller ändringarna som gjordes i filen "material.txt".

```
git checkout extramaterial
git branch
```

* Detta sätter den valda grenen till extramaterial. Ändringarna som sparades på grenen "master" syns ej längre.
* Redigera innehållet i "material.txt", förslagsvis genom att lägga till en rad med texten "Införskaffa ett riktigt bra stafli.". Spara sedan filen.

```
git commit --all --message "lägger till ett riktigt bra stafli i material"
git log --oneline
```

* Detta skapar en ny sparad ändring och lägger den efter den senaste sparade ändringen på den valda grenen (extramaterial). Den sparade ändringen innehåller ändringarna som gjordes i filen "material.txt".

```
git rebase master
git status
```

* Git klarar inte av att automatiskt ändra utgångspunkten för den valda grenen (extramaterial). Detta då liknande ändringar har gjorts parallellt i den valda grenen och i grenen till vilken utångspunkten försöker ändras.

> När Git upptäcker konflikter kommer Git att ändra berörda filer och markera raderna som orsakar konflikten med en speciell syntax. Här behöver du som användare välja vilken av de två ändringarna (eller en kombination av de båda!) som är korrekt. Du redigerar filen till önskat tillstånd och fortsätter sedan.

```
git add .
git rebase --continue
```
