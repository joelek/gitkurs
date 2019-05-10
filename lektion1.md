# Lektion 1: Ändringars tre tillstånd

I kursens första lektion lär vi oss att arbeta med Gits tre olika tillstånd för ändringar *states*. Dessa är *working directory* där alla nya ändringar du gör hamnar, *staging area* där alla ändringar du väljer hamnar samt *repository* där alla sparande ändringar hamnar. Efter lektionen kommer du att kunna använda Git för lokal, linjär versionshantering.

## 1. Initiera Git för Alice

* Skapa en tom katalog, förslagsvis med namnet "gitkurs-alice".
* Starta en terminal i katalogen, exempelvis genom att högerklicka och välja *Git Bash Here* som Windowsanvändare.

```
git init
git status
```

Detta initierar ett nytt Git-projekt i katalogen.

## 2. Nya filer hamnar i Gits *working directory*

* Skapa en tom fil med namn "material.txt" i katalogen.

```
git status
```

Filen "material.txt" ligger i Gits *working directory* och hanteras ännu ej av Git.

## 3. Nya filer kan väljas genom att adderas till Gits *staging area*

```
git add material.txt
git status
```

Innehållet som var sparat i filen "material.txt" då kommandot kördes ligger nu i Gits *staging area*.

## 4. Valda ändringar kan sparas i Gits *repository*

```
git commit --message "skapar material.txt"
git status
```

Allt som adderats till Gits *staging area* har nu sparats i Gits *repository*.

```
git log --oneline
```

Detta visar de senaste sparade ändringarna som finns i fallande kronologisk ordning.

```
git show head
```

Detta visar innehållet i den senaste sparade ändringen som finns.

## 5. Nya ändringar hamnar i Gits *working directory*

* Ändra innehållet i filen "material.txt", förslagsvis genom att lägga till en rad med texten "Införskaffa en blank canvas.". Spara sedan filen.

```
git status
```

Ändringarna som gjordes i filen "material.txt" ligger i Gits *working directory*.

```
git diff
```

Skillnaderna mellan Gits *working directory* och Gits *staging area* visas och är lika med ändringarna som gjordes i filen "material.txt".

```
git diff --staged
```

Skillnaderna mellan Gits *staging area* och Gits *repository* visas. Det finns inga skillnader.

## 6. Nya ändringar kan väljas genom att adderas till Gits *staging area*

```
git add material.txt
git status
```

Gits *staging area* inkluderar nu ändringarna som gjordes i "material.txt".

```
git diff
```

Skillnaderna mellan Gits *working directory* och Gits *staging area* visas. Det finns inga skillnader.

```
git diff --staged
```

Skillnaderna mellan Gits *staging area* och Gits *repository* visas och är lika med ändringarna som gjordes i filen "material.txt".

```
git commit --message "lägger till canvas i material.txt"
git log --oneline
```

Detta skapar en ny sparad ändring i Gits *repository*.

## 7. Valda ändringar i Gits *staging area* kan göras ovalda genom att flyttas tillbaka till Gits *working directory*

* Redigera innehållet i filen "material.txt", förslagsvis genom att lägga till en rad med texten "Införskaffa några penslar.". Spara sedan filen.

```
git status
git add material.txt
git status
```

Ändringarna som låg i Gits *working directory* valdes genom att adderas till Gits *staging area*.

```
git reset head material.txt
git status
```

Ändringarna som låg i Gits *staging area* flyttades tillbaka till Gits *working directory*.

## 8. Filer kan återställas till versioner sparade i Gits "repository"

```
git checkout -- material.txt
git status
```

Ändringarna som låg i Gits *working directory* togs bort för alltid då de aldrig sparades i Gits *repository*.

## 9. Ändringar sparade i Gits *repository* kan uppdateras

* Redigera innehållet i filen "material.txt" en gång till, förslagsvis genom att lägga till en rad med texten "Införskaffa några penslar.". Spara sedan filen.

```
git status
git add material.txt
git status
```

Ändringarna i Gits *working directory* valdes genom att adderas till Gits *staging area*.

```
git commit --amend --no-edit
git log --oneline
```

De valda ändringarna i Gits *staging area* tillfördes den senaste sparade ändringen utan att meddelandet för ändringen ändrades.

## 10.  Meddelanden sparade i Gits *repository* kan uppdateras

```
git show head
```

Meddelandet för den senaste sparade ändringen passar inte längre som beskrivning av det som ändrats.

```
git diff --staged
```

Skillnaderna mellan Gits *staging area* och Gits *repository* visas. Det finns inga skillnader.

```
git commit --amend --message "lägger till saker i material.txt"
git show head
```

Gits *staging area* är tom så kommandot ändrar endast meddelandet för den senaste sparade ändringen.
