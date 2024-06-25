---
path: '/osa-3/3-mer-om-loopar'
title: 'Mera om loopar'
hidden: false
---

<text-box variant='learningObjectives' name='Lärandemål'>

Efter den här delen

* vet du när `break`-kommandot behövs för att avsluta en loop
* kan du använda `continue`-kommandot för att fortsätta till nästa iteration
* förstår du hur kapslade loopar fungerar.

</text-box>

## `break`-kommandot

Du har redan bekantat dig med `break`-kommandot. Det kan användas för att direkt avsluta en loop. Ett exempel på ett användningsområde för `break`-kommandot är då man ber användaren om någon information och loopen ska avslutas när ett visst värde ges.

Samma funktionalitet kan skapas utan `break`-kommandot med ett passligt villkor. De här två programmen ber användaren ge siffor som adderas ihop tills användaren skriver siffran -1.

```python
# version 1 med break-kommando

summa = 0

while True:
    siffra = int(input("Ge ett tal, -1 avslutar programmet: "))
    if siffra == -1:
        break
    summa += siffra

print (f"Summan är {summa}")
```

```python
# version 2 utan break-kommando

summa = 0
siffra = 0

while siffra != -1:
    siffra = int(input("Ge ett tal, -1 avslutar programmet: "))
    if siffra != -1:
        summa += siffra

print (f"Summan är {summa}")
```

Båda programmen skriver ut samma saker med samma indata, exempelvis:

<sample-output>

Ge ett tal, -1 avslutar programmet: **2**
Ge ett tal, -1 avslutar programmet: **4**
Ge ett tal, -1 avslutar programmet: **5**
Ge ett tal, -1 avslutar programmet: **3**
Ge ett tal, -1 avslutar programmet: **-1**
Summan är 14

</sample-output>

Båda programmen är alltså identiska till deras funktion men den första metoden är ofta enklare eftersom villkoret `siffra == 1` endast finns på ett ställe och variabeln `siffra` behöver inte initieras utanför loopen.

`break`-kommandot kan kombineras med ett passligt villkor. Till exempel följande loop upprepas så länge summan av siffrorna är högst 100, men avslutas också då man ger siffran -1.

Så här kan det se ut när programmet körs:

```python
summa = 0

while summa <= 100:
    siffra = int(input("Ge ett tal, -1 avslutar programmet: "))
    if siffra == -1:
        break
    summa += siffra

print (f"Summan är {summa}")
```

Exempel:

<sample-output>

Ge ett tal, -1 avslutar programmet: **15**
Ge ett tal, -1 avslutar programmet: **8**
Ge ett tal, -1 avslutar programmet: **21**
Ge ett tal, -1 avslutar programmet: **-1**
Summan är 44

</sample-output>

<sample-output>

Ge ett tal, -1 avslutar programmet: **15**
Ge ett tal, -1 avslutar programmet: **8**
Ge ett tal, -1 avslutar programmet: **21**
Ge ett tal, -1 avslutar programmet: **45**
Ge ett tal, -1 avslutar programmet: **17**
Summan är 106

</sample-output>

I det första exemplet avslutas loopen eftersom användaren ger siffran -1. I det andra exemplet avslutas loopen eftersom summan blir större än 100.

Som alltid inom programmering finns det flera sätt att uppnå samma resultat. Följande program fungerar på identiskt sätt jämfört med de två exemplen ovan:

```python
summa = 0

while True:
    siffra = int(input("Ge ett tal, -1 avslutar programmet: "))
    if siffra == -1:
        break
    summa += siffra
    if summa > 100:
        break

print (f"Summan är {summa}")
```

## `continue`-kommandot

Ett annat sätt att påverka hur en loop körs är `continue`-kommandot. Det får loopen att hoppa till början, där villkoret för loopen finns. Loopen fortsätter köra normalt därifrån börjandes från att kolla villkoret:

<img src="3_3.png">

Till exempel följande program adderar siffor som användaren ger, men bara då den givna siffran är mindre än tio. Om siffran är tio eller större, hoppar man till början av loopen utan att addera siffran.

```python
summa = 0

while True:
    siffra = int(input("Ge ett tal, -1 avslutar programmet: "))
    if siffra == -1:
        break
    if siffra >= 10:
        continue
    summa += siffra

print (f"Summan är {summa}")
```

<sample-output>

Ge ett tal, -1 avslutar programmet: **4**
Ge ett tal, -1 avslutar programmet: **7**
Ge ett tal, -1 avslutar programmet: **99**
Ge ett tal, -1 avslutar programmet: **5**
Ge ett tal, -1 avslutar programmet: **-1**
Summan är 16

</sample-output>

## Kapslade loopar

Precis som med if-satser kan loopar placeras inom andra loopar. Till exempel följande program använder sig av en loop för att fråga efter en siffra från användaren. Inom den här loopen finns en annan loop som räknar ner från det givna talet till ett:

```python
while True:
    siffra = int(input("Ge ett tal: "))
    if siffra == -1:
        break
    while siffra > 0:
        print(siffra)
        siffra -= 1
```

<sample-output>

Ge ett tal: **4**
4
3
2
1
Ge ett tal: **3**
3
2
1
Ge ett tal: **6**
6
5
4
3
2
1
Ge ett tal: **-1**

</Sample-output>

I kapslade loopar är det bra att märka att `break` och `continue` endast påverkar den innersta loopen de är i. Föregående exemplet skulle kunna skrivas så här:

```python
while True:
    siffra = int(input("Ge ett tal: "))
    if siffra == -1:
        break
    while True:
        if siffra <= 0:
            break
        print(siffra)
        siffra -= 1
```

Här avslutar det andra `break`-kommandot endast den inre loopen som används för att skriva ut siffrorna.

## Hjälpvariabler med loopar

Vi har redan använt oss av hjälpvariabler – som ökar eller minskar för varje iteration av en loop – flera gånger, så följande program borde till sin struktur se ganska bekant ut. Programmet skriver ut alla jämna tal från noll fram till det tal som användaren angett:

```python
grans = int(input("Ge ett tal: "))
i = 0
while i < grans:
    print(i)
    i += 2
```

<sample-output>

Ge ett tal: **8**
0
2
4
6

</sample-output>

Hjälpvariabeln `i` har tilldelats värdet 0 före loopen, som ökar på talet med två för varje iteration.

När man använder kapslade loopar kan det uppstå ett behov för en ny hjälpvariabel för den inre loopen. Följande program skriver ut en "sifferpyramid" baserat på den siffra som användaren angett:

```python
siffra = int(input("Ge ett tal: "))
while siffra > 0:
    i = 0
    while i < siffra:
        print(f"{i} ", end="")
        i += 1
    print()
    siffra -= 1
```

<sample-output>

Ge ett tal: **5**
0 1 2 3 4
0 1 2 3
0 1 2
0 1
0

</sample-output>

I programmet använder den yttre loopen hjälpvariabeln `siffra` som minskar med ett tills det når till noll. Hjälpvariabeln `i` tilldelas värdet 0 före man fortsätter till den inre loopen – varje gång den yttre loopen upprepas.

Den inre loopen använder sig av hjälpvariabeln `i` som ökar med talet 1 för varje iteration av den inre loopen. Den inre loopen fortsätter tills `i` är lika med `siffra`, och skriver ut varje värde hos `i` med mellanslag emellan. När loopen avslutas skapar `print`-kommandot i den yttre loopen en ny rad.

I och med att värdet på `siffra` minskar för varje iteration av den yttre loopen, kommer antalet iterationer hos den inre loopen att minska. Vid varje upprepning blir sifferraden kortare, vilket bildar "pyramiden".

Kapslade loopar kan vara svårtolkade på en första titt, men det är viktigt att förstå hur de fungerar. Du kan använda dig av Python Tutors [visualiseringsverktyg](https://pythontutor.com/visualize.html) för att bättre förstå hur ovanstående exempel fungerar. Kopiera koden ovan till kodfönstret och följ hur utskriften formar sig och hur hjälpvariablernas värden ändras medan programmet körs.

<in-browser-programming-exercise name="Multiplikationstabell" tmcname="osa03-15b_multiplikationstabell">

Skapa ett program som ber om ett positivt heltal från användare. Programmet ska skriva ut multiplikationsoperationer fram till talet, enligt exemplen nedan:

<sample-output>

Ge ett tal: 2
1 x 1 = 1
1 x 2 = 2
2 x 1 = 2
2 x 2 = 4

</sample-output>

<sample-output>

Ge ett tal: 3
1 x 1 = 1
1 x 2 = 2
1 x 3 = 3
2 x 1 = 2
2 x 2 = 4
2 x 3 = 6
3 x 1 = 3
3 x 2 = 6
3 x 3 = 9

</sample-output>

</in-browser-programming-exercise>


<in-browser-programming-exercise name="Ordens första bokstäver" tmcname="osa03-16_forsta_bokstaverna">

Skapa ett program som ber användaren ange en mening. Programmet skriver därefter ut den första bokstaven i varje ord på sin egen rad.

Exempel:

<sample-output>

Ge en mening: **Kira gillade klara glaskulor**
K
g
k
g

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Fakulteter" tmcname="osa03-17_fakulteter">

Skapa ett program som ber användaren ange ett heltal. Om talet är negativt eller noll, avslutas programmet. I övriga fall skriver programmet ut talets fakultet.

Fakultet räknas genom att multiplicera talet med sig själv samt alla mindre positiva heltal. Fakulteten för 5 är t.ex. `1 * 2 * 3 * 4 * 5 = 120`.

Exempel:

<sample-output>

Ge ett tal: **3**
Talets 3 fakultet är 6
Ge ett tal: **4**
Talets 4 fakultet är 24
Ge ett tal: **-1**
Tack och hej!

</sample-output>

<sample-output>

Ge ett tal: **1**
Talets 1 fakultet är 1
Ge ett tal: **0**
Tack och hej!

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Sväng paren" tmcname="osa03-18_svang_paren">

Skapa ett program som skriver ut talen från ett till det tal användaren angett. Talen ska parvis vara omvända.

<sample-output>

Ge ett tal: **5**
2
1
4
3
5

</sample-output>

<sample-output>

Ge ett tal: **6**
2
1
4
3
6
5

</sample-output>

</in-browser-programming-exercise>

<in-browser-programming-exercise name="Turvis" tmcname="osa03-19_turvis">

Skapa ett program som ber användaren ange ett tal. Programmet ska skriva ut talen turvis enligt följande exempel:

<sample-output>

Ge ett tal: **5**
1
5
2
4
3

</sample-output>

<sample-output>

Ge ett tal: **6**
1
6
2
5
3
4

</sample-output>

</in-browser-programming-exercise>

<quiz id="c7b69cde-08a4-5de2-9d23-3315903be6ec"></quiz>
