# Lektion 1: Tre *states*

I den första lektionen av kursen lär vi oss att arbeta med Gits tre olika *states*. Dessa är *working directory* där alla nya ändringar du gör hamnar, *staging area* där alla ändringar du väljer hamnar samt *repository* där alla sparande ändringar hamnar. Efter lektionen kommer du att kunna använda Git för lokal linjär versionshantering.

## 1. Initiera Git

* Skapa en tom katalog.
* Starta en terminal i katalogen, exempelvis genom att högerklicka och välja *Git Bash Here* som Windowsanvändare.

```
git init
git status
```

* Detta initierar ett nytt Git-projekt i katalogen.

## 2. Nya filer hamnar i Gits *working directory*

* Skapa en tom fil med namn "picasso.txt" i katalogen.

```
git status
```

* Filen "picasso.txt" ligger i Gits *working directory* och hanteras ännu ej av Git.

## 3. Nya filer kan väljas genom att adderas till Gits *staging area*

```
git add picasso.txt
git status
```

* Innehållet som var sparat i filen "picasso.txt" då kommandot *git add picasso.txt* kördes ligger nu i Gits *staging area*.

## 4. Nya ändringar hamnar i Gits *working directory*

* Ändra innehållet i filen "picasso.txt", förslagsvis genom att skriva "hämta en tom canvas\n\n". Spara sen filen.

```
git status
```

* Det som ligger i Gits *staging area* har inte förändrats.
* Ändringarna som gjordes i filen "picasso.txt" ligger i Gits *working directory*.

```
git diff
```

* Skillnaderna mellan Gits *staging area* och Gits *working directory* visas och är lika med ändringarna som gjordes i filen "picasso.txt".

```
git diff --staged
```

* Skillnaderna mellan Gits *repository* och Gits *staging area* visas. Det finns inga skillnader.

## 5. Nya ändringar kan väljas genom att adderas till Gits *staging area*

```
git add picasso.txt
git status
```

* Gits *staging area* inkluderar nu ändringarna som gjordes i "picasso.txt".

```
git diff
```

* Skillnaderna mellan Gits *staging area* och Gits *working directory* visas. Det finns inga skillnader.

```
git diff --staged
```

* Skillnaderna mellan Gits *repository* och Gits *staging area* visas och är lika med ändringarna som gjordes i filen "picasso.txt".

## 6. Valda ändringar kan sparas i Gits *repository*

```
git commit --message "canvas"
git status
```

* Allt som tidigare adderades till Gits *staging area* har nu hamnat i Gits *repository*.

```
git log
```

* Visar de senaste sparade ändringarna som finns i den aktiva grenen (master) i fallande kronologisk ordning.

```
git show head
```

* Visar innehållet i den senaste sparade ändringen som finns i den aktiva grenen (master).

## 7. Valda ändringar i Gits *staging area* kan göras ovalda genom att flyttas tillbaka till Gits *working directory*

* Redigera innehållet i filen "picasso.txt", förslagsvis genom att ändra innehållet till "hämta en tom canvas\n\nhämta några penslar\n\nhämta lite färg\n\n".

```
git status
git add .
git status
```

* Ändringarna som låg i Gits *working directory* valdes genom att adderas till Gits *staging area*.

```
git reset head
git status
```

* Ändringarna som låg i Gits *staging area* flyttades tillbaka till Gits *working directory*.

## 8. Filer kan återställas till versioner sparade i Gits "repository"

```
git checkout -- .
git status
```

* Ändringarna som låg i Gits *working directory* togs bort för alltid då de aldrig sparades i Gits *repository*.

## 9. Ändringar sparade i Gits *repository* kan justeras

* Redigera innehållet i filen "picasso.txt" en gång till, förslagsvis genom att ändra innehållet till "hämta en tom canvas, några penslar och lite färg\n\n".

```
git status
git add .
git status
```

* Ändringarna i Gits *working directory* valdes genom att adderas till Gits *staging area*.

```
git commit --amend --no-edit
git status
```

* De valda ändringarna i Gits *staging area* tillfördes den senaste sparade ändringen som finns i den aktiva grenen (master) utan att meddelandet för ändringen ändrades.

## 10.  Meddelanden sparade i Gits *repository* kan justeras

```
git status
git log
git show head
```

* Meddelandet för den senaste sparade ändringen passar inte längre innehållet.

```
git status
git commit --amend --message "material"
git status
```

* Gits *staging area* är tom så kommandot ändrar endast meddelandet för den senaste sparade ändringen i den aktiva grenen (master) till "material".
